* <meta name=" viewport" content= "width=device-width, initial-scale=1.0" />
* CSS selector
    1. element selector
    2. id selector
    3. class selector
    4. group selector
    5. Input [type="checkedbox"].toggle:checked + lable {}
6

7. Aspect-ratio: 1/1; it is reset height/width respect to width/height.
8. Clamp (min , valueRespectTo you screen , max);
9. Focus-within()
10. place-items: center
10. Display: grid
    * grid-template-columns: repeat(4, 100px);
    * grid-template-columns: repeat( auto-fit/auto-fill, minmax(200px, 1fr)
    * grid-auto-rows: minmax(150px, auto);
    * grid-template-rows: for all;
    * grid-row-gap:
    * grid-column-gap:
    * grid-gap:
    * grid-area{
    * }
    * child 
        • grid-column-start: 1;
        • grid-column-end: 2;
        • grid-column: 1/-1;
        • grid-column: span 2;
        • same as grid-row-start;
        • grid-item-2;
        • justified - content: center,start,end
        • justified-self:
        • align-self:
        • grid-flow-row-dense
        • place-items: center
12. @media(min-width: 300px)
         • @media( width >= 300px)
         • @media( orientation: landscape)
         •  @media( orientation: portrait)
         •  @media( min-aspect-ratio : 16/9)
         •  @media(
         •  .container {
               container-type: inline
             }
         • @container ( min-width: 300px)
13.
8. CSS Unit :
      px
      % : relatives to parents
      em : 1em = 100%
      rem : root relatives 
        * it is relative to parent font size
      fw/fh : fraction size
9. text-align:
* Background: background-attachment/background-repeat
* Border:
      Border-style: Top Left Button Right;
      Border-top-style: value;
      Border-color:
      Border-width:
* box-shadow: none|h-shadow v-shadow blur spread color |inset|initial|inherit;
* text-shadow:
* transition : width 3 s ;
* Display Properties
    Display : block/ inline/Inline-block/none;
* Position
      position: static/relative/absolute/fixed
* Font Styling
      font-family:
      font-size:
      font-weight:
      line-height:
      float: float aside from img
* Z-index:
* Transparency / Opacity 
1. Linear Gradients  :
    Options in direction:
         goesdown
         up
         left
         right
         diagonally
         Deg
    background: linear-gradient(direction,      
    color-stop1, color-stop2, ...);
    
2. Radial Gradients (defined by their center)
       background: radial-gradient(circle, green,
       yellow, blue);
* Transition:
       transition: property_name duration function
* animation:
       • Keyframes{
            from/to{}
            0% /100{}
       }
       • animation: animation-name animation-duration animation-timing-function animation-delay animation-iteration-count animation-diraction
* Object-fit: fill/cover/contain/none/scale-down
* object-position: x/y; %/we
* Mask-image:
    * mask-image: url()/lineargradiant
    * mask-repeat: no-repeat/
* flex box
    * Parent container
        * display: flex;
        * Flex: value of division;
        * flex-direction: column/row
        * justified-content:
            centre/flex-end/flex-start
            space- evenly space-around    
            space-between.
        * align-item: centre/
        * Gap: 2rem;
        * flex-wrap: wrap/ wrap-reverse;
        * flex-flow: column wrap;
        * Writingmode: (vertical/ horizontal )-rl/lr
        * Align-contents: center (use with wrap with specific height of parents container)
    * Child container {
        * Flex-grow:
        * Flex-skrink:
        * Flex-basis: (measure widths)
        * Flex: grow skrink basis
        * Margin effect
          Margin-right : auto
        }   
        * flex- items (
            order
            flex-grow:
            flex-srick:
            align-self: center;//
* Media Query
    @media(min-width: value1)and(max
    -width: value2){  }
* Container
    * Class {
        * Container-type: size/inline-size;
        * Container-name: mainContainer
          • container-unit - cqw
          }
    * @container containerName ( width value) {
    }
•
* Pseudo Class
* # Direct we can use
    * scale: top/buttom left/right z-direction;
    * translate: x y z;
    * rotate: 1 1 1 45deg;
* root: {
        --VariableName: value;
    }
* window.getConputedStyle(document.documentElement).getPropertyValue('css-variable-nams')
* documents.getElementById('light-bule').addEventListner("click"){ 
    * document.documentelement).setPropertyValue('--div-background-color', pink);
}
* Overflow
   • scroll-nap-type: x/y mandatory/priority;
       • // to container
   • scroll-nap-align: center,
* Resize container
     • overflow: auto;
     • resize: both;
* truncating using css
     • cutting of words in an article
     • display : -webkit-box;
     • -webkit-line-clamp: 1;
     • -webkit-box-orient: vertical;
     • Overflow: hidden;
•
* written-
* Animation on Scoll
    * Scroll-timeline element-move {
          //Watch Animation on api
     }
    * intersection observer api
          • It check visible on screen on not
          • const observe = new IntersectionObserver((entries) => {
               • entries.forEach((entry) => {
                    Log(entry)
                    If (entry.isIntersection) {
                        entry.target.classList.add('show');
                    } else {
                        entry.target.classList.remove('show')
                    }
               • }
           }
           • const hiddenElements = document.querySelectorAll('.hidden');
           • hiddenElements.forEach((el) => oberver.observe(el));
     •
1600px
1199px
991px
767px
575px
* Responsive
    * max-width 
    * rem
        * parent font-size = 10;
    * %
    * vw and vh
        * height: vw
    * media query
        * global
        * laptop media query
        * tablet media query
        * mobile media query
        * @media (max-width: 1200px) {

        }
    * CSS grid
        * flex in 1D
        * grid in 2D
            * parent container
                * display : grid;
                * grid-template-columns: 300px 200px 200px;
                * grid-template-rows: 500px 400px;
                * justify-items: start;
                * align-items: center;
                * justify-content: center;
                * align-content: center;
                * gap: ;
                * row-gap: ;
                * column-gap: ;
            * concept
                * grid lines
                * grid track
                * grid shell
                * fractional unit
                    * grid-template-columns: repeat(3, 1fr);
                    * grid-auto-rows: 4rem;
                * 
            * children
                * grid-column-start: span 2;
                * 















