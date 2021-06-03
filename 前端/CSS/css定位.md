## static 定位 

  HTML 元素的默认值，即没有定位，遵循正常的文档流对象。 

  静态定位的元素不会受到 top, bottom, left, right影响。 

##    fixed 定位  

   元素的位置相对于浏览器窗口是固定位置。  

   即使窗口是滚动的它也不会移动：  

##    relative 定位  

   相对定位元素的定位是相对其正常位置。  

##    absolute 定位  

   绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于<html>:  

   absolute 定位使元素的位置与文档流无关，因此不占据空间。  

   absolute 定位的元素和其他元素重叠。  

##    sticky 定位  

   sticky 英文字面意思是粘，粘贴，所以可以把它称之为粘性定位。  

   **position: sticky;** 基于用户的滚动位置来定位。  

   粘性定位的元素是依赖于用户的滚动，在 **position:relative** 与 **position:fixed** 定位之间切换。  

   它的行为就像 **position:relative;** 而当页面滚动超出目标区域时，它的表现就像 **position:fixed;**，它会固定在目标位置。  

   元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。  

   这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。



