* # Intersection Observer
    * <div class="card_container">
        <div class="card"></div>
        ....
        </div>
    * script
        * const cards = document.querySelectorAll(".card")
        * const observer = new IntersectionObserver( entries => {
            * enteries.forEach(entry => {
                entry.target.classList.toggle("show", entry.isIntersection)
                if(entry.isIntersection) observer.unobserve(entry.target) // it stop observing it once it on screen  
            }) 
            * }, {
                threshold: 1, // it visible % value
                rootMargin: "-100px" , // it is screen margin
                root: // it is used to define the container
            })
            * entries
                * Array(1)
                    * every thing observing
                    * boundingClientRect
                    * intersectionRatio: 1 //100% on screen
                    * intersectionRect
                    * isIntersection:true
                    * target : div.card.show
                    * 
        
        * lazing loader
            * const lastcardObserver = new IntersectionObserver( entries => {
                const lastCard =entries[0]
                if(!lastCard.isIntersection) return loadNewCard()
                * lastCardObserver.unobserver(lastCard.target) 
                    * // it remove current card over because the last card change
                * lastcardObserver.observe(document.querySelect("card:last-card"))
                    * it set to new last card
            },{
                rootmargin: "100px"
            })

        * cards.forEach(card => {
            observer.observe(card)
        })
            // it observer every card
        * const cardContainer =document.querySelect(".card-container")
        * function loadNewCards() {
            for(let i = 0; i < 10; i++) {
                const card = document.createElement("div")
                card.textContent = "New Card"
                card.classList.add("card")
                observer.observe(card)
                cardContainer.append(card)
            }
        }

* # Mutation Observer
    * it trigger the function on any type of mutation has occurs in observer
    * const mutationObserver = new MutationObserver( entries => {

    })
    * entries => {
        // it is return array of changes
        * triger
        * type: "trigger options"
        * removedNodes
        * addedNodes


    }
    * const parent = document.querySelect(".parent")

    * mutationObserver.observe(parent, {option}
        * options
            * children: "true" 
                * // it trigger function of change of children
            * attributes: true
                * any type of attributes change on any parent and children
            * attributesOldValue: true
                * it show prev value of attribute
            * attributeFilter: ["id","name"]
                * it only observe that attribute
            * characterData: true
                * data change child node
                    * eg
                        <div class="parent>
                        <div class="child">nodeValue<div>
                        </div>
                        * mutationObserver.observe(parent.children[0].childNode[0])
                        * then it trigger on Node value change
            * characterDataOldValue: true
            * subtree: true
                * it check option in depth on children and sub children
                * option check that option on children also


    * mutationObserver.disconnect()
        * to stop change

    * you can use multi instance of observer object of that MutationObserver class
    *

* Resive Observer
    * const box = document.querySelector(".box")
    * const container = document.querySelect(".container")
    * const observer = new ResizeObserver((entries) => {
        const boxElement = entries[0]
        const isSmall = boxElement.contentReact.width < 150
        boxElement.target.style.backgroundColor = isSmall ? "blue" : "red"
    })
    * observer.observe(box)
    * observer.observe(container)
