## JQeury -> React


```ts

function tabScrollerPosition() {
    $('.tab_list').each(function() { // for 문
        let $li = $(this).find('.tab_item');
        let idx: any, gap;
        $li.each(function(i) {
            if($(this).hasClass('selected')) idx = i;
            return idx;
        });
        if ($li.eq(idx) !== undefined) {
            let posX = $li.eq(idx).offset()?.left; //.offset() 좌표 가져와서 이동 시키는데 x 축 위치 가져올 때 left
            let $wrap = $li.closest('.tab_list'); // 요소 1개 선택
            if (posX != null) {
                $wrap.scrollLeft(posX);
            }
        }
    });
}

```



```ts

    const scrollRef = useRef(null)

    const onClickTest = () => {
        const list = document.querySelectorAll(".tab_item");
        const listTab = document.querySelector(".tab_list");
        list.forEach( (value) => {
            if (value.classList.contains("selected")){
                const position = value.getBoundingClientRect();
                if (listTab?.scrollLeft != null)
                    listTab.scrollLeft = position.x;
            }
        })
    }

    return (
        <nav id="menuTab">
            <ul className="tab_list" onClick={onClickTest} ref={scrollRef}>
                <li className={tabState === "OverView" ? "tab_item selected" : "tab_item"} ><Link to={"/"}  id={"Overview"}>Overview</Link></li>
                <li className={tabState === "Templates" ? "tab_item selected" : "tab_item"} ><Link to={"/"} id={"Templates"} >Templates</Link></li>
                <li className={tabState === "Products" ? "tab_item selected" : "tab_item"}><Link to={"/"} id={"Products"}>Products</Link></li>
                <li className={tabState === "Settings" ? "tab_item selected" : "tab_item"}><Link to={"/"} id={"Settings"}>Settings</Link></li>
            </ul>
        </nav>
    )
```
## 이 코드가 틀리다면 알려주세요.. JQuery 넘 어렵따. 

1. .getBoundingClientRect() -> Document Element 좌표 값 가져오는 함수

2. 타입스크립트에서 listTab.scrollLeft 를 ? 문법으로 처리하지 못하는 이유가 무엇일까.
