Enable larger video frame on Church Online Platform

DESCRIPTION



## The Code
##### Custom CSS
```css
/**
* Enable bigger video frame when window size exceeds 1200px
*/
@media (min-width:1200px){
  .row {
    width: 1200px;
  }
  #main .six {
    width: 55%;
  }
  #main .five {
    width: 44.6667%
  }
  #media {
    width: 640px;
  }
  #media .video {
    width: 640px;
  }
}
```
##### Custom Javascript
```javascript
/**
 * This eliminates stretched slides when using the larger video size
 * 
 * When at the larger video size, this swaps out the 'cropped' slides that ChOP
 * creates (480px wide) with the original uploaded file.
 * You must make sure you're uploading files that are 640px wide!
 */ 
(function(){
    $(document).ready(function(){ 
        // Wait for system to load, hopefully bind to slide_area for image swapout
        setTimeout(function(){
            var $slide_area = $( "#slide_area" );

            $slide_area.on('DOMNodeInserted', function(e) { 
                //A new slide appeared!
                if($slide_area.width() > 480){
                    $slide_area.css('opacity', 0.00);
                    var bg = $(e.target).css('background-image').replace('/slide/', '/original/');

                    $(e.target).css('background-image', '');    //Remove the one we don't want
                    
                    var $slide_image = $('.slide_image', $slide_area);
                    $slide_image.on('DOMNodeInserted', function(e){ e.stopPropagation(); });
                    $slide_image.append('<div id="slide_image_custom"></div>');
                    $('#slide_image_custom').css('background-image', bg);
                    $slide_area.fadeTo(400, 1.0);
                }
            });
        }, 3000);
    });
})();

```
