# knowledge

### React
- 버튼 클릭 시 다음 section으로 넘어갈 때
``` React
import { useRef } from 'react'

const ref = useRef(null);

const scrollNextSection = () => {
    ref.current.scrollIntoView({ behavior: "smooth" });
}

return <div ref={ref} onCilck={scrollNextSection}></div>
```
