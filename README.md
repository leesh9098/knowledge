# knowledge

### React
- React 프로젝트 내부에서 script 태그 사용시에 필요한 hook 함수 (초기화)
``` JSX
import { useState, useEffect } from "react";

function useScript(src) {
	// Keep track of script status ("idle", "loading", "ready", "error")
	const [status, setStatus] = useState(src ? "loading" : "idle");

	useEffect(
		() => {
			// Allow falsy src value if waiting on other data needed for
			// constructing the script URL passed to this hook.
			if (!src) {
				setStatus("idle");
				return;
			}

			// Fetch existing script element by src
			// It may have been added by another intance of this hook
			let script = document.querySelector(`script[src="${src}"]`);

			if (!script) {
				// Create script
				script = document.createElement("script");
				script.src = src;
				script.async = true;
				script.setAttribute("data-status", "loading");
				// Add script to document body
				document.body.appendChild(script);

				// Store status in attribute on script
				// This can be read by other instances of this hook
				const setAttributeFromEvent = (event) => {
					script.setAttribute(
						"data-status",
						event.type === "load" ? "ready" : "error"
					);
				};

				script.addEventListener("load", setAttributeFromEvent);
				script.addEventListener("error", setAttributeFromEvent);
			} else {
				// Grab existing script status from attribute and set to state.
				setStatus(script.getAttribute("data-status"));
			}

			// Script event handler to update status in state
			// Note: Even if the script already exists we still need to add
			// event handlers to update the state for *this* hook instance.
			const setStateFromEvent = (event) => {
				setStatus(event.type === "load" ? "ready" : "error");
			};

			// Add event listeners
			script.addEventListener("load", setStateFromEvent);
			script.addEventListener("error", setStateFromEvent);

			// Remove event listeners on cleanup
			return () => {
				if (script) {
					script.removeEventListener("load", setStateFromEvent);
					script.removeEventListener("error", setStateFromEvent);
				}
			};
		},
		[src] // Only re-run effect if script src changes
	);

	return status;
}

export { useScript };
```

- 버튼 클릭 시 다음 section으로 넘어갈 때
``` JSX
import { useRef } from 'react'

const ref = useRef(null);

const scrollNextSection = () => {
    ref.current.scrollIntoView({ behavior: "smooth" }); // 부드러운 화면 
}

return <div ref={ref} onCilck={scrollNextSection}></div>
```

- ScrollAnimation 라이브러리 사용법
``` JSX
// npm install react-animate-on-scroll --save
import ScrollAnimation from "react-animate-on-scroll";

<ScrollAnimation
    offset={} // default 150, px단위
    animateIn="animate__fadeIn" // viewport안에 들어올 때 적용되는 animation ※'animate__'를 붙여줘야 적용됨
    animateOut="animate__fadeOut" // viewport를 벗어날 때 적용되는 animation
```
- Node JS 서버와 통신할 때 필요한 Proxy (setupProxy.js)
``` JSX
// src폴더 안에 파일 생성
// package.json에 "proxy": "url" 추가
const { createProxyMiddleware } = require('http-proxy-middleware')
module.exports = function (app) {
    app.use(createProxyMiddleware('/path', {
        target: 'url'
        // changeOrigin: true
    }));
}
```

- express 서버 통신
``` JavaScript
// npm install express --save
// npm install cors --save
const express = require("express");
const app = express();
const cors = require("cors");
const port = 3001; // 포트 설정

app.use(cors())
app.use(express.urlencoded({ extended: true }));
app.use(express.json());

app.post('path or url', (req, res) => {
    res.send({data: req.body.data});
});

app.listen(port, () => {
    console.log(`listening on ${port}`);
});
```

### JavaScript
- PC 브라우저에서 뒤로가기 버튼 비활성화
``` JavaScript
{/*window.*/}history.pushState(null, null, {/*window.*/}location.href);
 window.onpopstate = () => {
    {/*window.*/}history.go(1);
};
```
- 브라우저의 localStorage와 sessionStorage 사용법
``` JavaScript
// item 저장
window.localStorage.setItem(key, value);
window.sessionStorage.setItem(key, value);

// item 가져오기
window.localStorage.getItem(key);
window.sessionStorage.getItem(key);

// item 일부 삭제
window.localStorage.removeItem(key);
window.sessionStorage.removeItem(key);

// item 전체 삭제
window.localStorage.clear();
window.sessionStorage.clear();
```
