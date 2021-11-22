# knowledge

### React
- 버튼 클릭 시 다음 section으로 넘어갈 때
``` JavaScript
const ref = useRef(null)

const scrollNextSection = () => {
    ref.current.scrollIntoView({ behavior: "smooth" })
}
```
