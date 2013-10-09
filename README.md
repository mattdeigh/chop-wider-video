Enable larger video frame on Church Online Platform

This code can be used to serve a larger video to users with larger displays. We implemented this at live.sandalschurch.com and saw fewer users taking the video full screen and more users engaging with the chat.

Most video embeded with iframes will automatically expand to fill the larger area, but you may need to check with your video hosting provider.


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
 * At the larger video size, this swaps out the 'cropped' slides that ChOP creates (480px wide)
 * with the original uploaded file. To make this work you must uploading images that are 640px
 * wide with the content in the center 480px. See slide_640.psd for a template.
 * 
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
