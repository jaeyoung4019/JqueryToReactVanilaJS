## JQeury Function 을 React 에서 사용할 수 있도록 만들겠습니다.


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

원래 함수는 이렇게 만들고 Document.ready 상황일 때 실행하도록 되어 있었습니다. 버튼 클릭시 새로 스크롤을 잡아줘야하기 때문에 버튼 클릭 시마다 실행하도록 변경하기 위해서 React 용 코드로 변경하였습니다.

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

이런 식으로 변경하였고 x 축을 가져오는 함수인 .getBoundingClientRect() 가 존재하는 것을 안 시간이였습니다.

이 외에 궁굼한 점은

다만 타입스크립트에서 listTab.scrollLeft 를 ? 문법으로 처리하지 못하는 것이 궁금할 뿐입니다!.
