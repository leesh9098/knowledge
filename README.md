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

- PC 브라우저에서 뒤로가기 버튼 비활성화
``` JavaScript
 {/*window.*/}history.pushState(null, null, {/*window.*/}location.href);
 window.onpopstate = () => {
    {/*window.*/}history.go(1);
};
```
