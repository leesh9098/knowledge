# knowledge

### React
- 버튼 클릭 시 다음 section으로 넘어갈 때
``` JSX
import { useRef } from 'react'

const ref = useRef(null);

const scrollNextSection = () => {
    ref.current.scrollIntoView({ behavior: "smooth" }); // 부드러운 화면 
}

return <div ref={ref} onCilck={scrollNextSection}></div>
```

- Node JS 서버와 통신할 때 필요한 Proxy (setupProxy.js)
``` JSX
// src폴더 안에 파일 생성
// package.json에 "proxy": "url" 
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
