# knowledge

### React
- 버튼 클릭 시 다음 section으로 넘어갈 때
``` JSX
import { useRef } from 'react'

const ref = useRef(null);

const scrollNextSection = () => {
    ref.current.scrollIntoView({ behavior: "smooth" });
}

return <div ref={ref} onCilck={scrollNextSection}></div>
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
