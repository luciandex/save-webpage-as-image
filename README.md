# save-webpage-as-image
Minimal configuration for saving a webpage as image using canvas

```html
<html>
    <body>
        <button onclick="saveAsImage()">Save as image</button>
    
        <!-- required hidden link -->
        <a id="downloadLink" href=""></a>
    
        <div id="element-to-save">
            <!-- all the content here -->
    
          <!-- an ignored element -->
          <div data-html2canvas-ignore></div>
        </div>
        
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
        <!-- <script src="https://cdn.jsdelivr.net/npm/canvas2image@1.0.5/canvas2image.min.js"></script> -->
        
        <script>
          function saveAsImage() {
              let date = new Date().toISOString().split('T')[0];
    
              /** @see https://www.semicolonworld.com/question/19446/how-to-set-custom-file-name-when-exporting-html-element-to-png-file-using-html2canvas-in-jquery */
              html2canvas(document.querySelector("#element-to-save")).then(canvas => {
                  let url = canvas.toDataURL();
                  jQuery("#downloadLink").attr({"href": url, "download": date + "_some_other_text"})
                      .on("click", function() {$(this).remove()})
                      .appendTo("body")[0].click()
              })
          
              /** This works fine, but there is no way to change file name */
              // html2canvas(document.querySelector("#element-to-save")).then(canvas => {
              //     // Canvas2Image.saveAsPNG(canvas);
              //     Canvas2Image.saveAsJPEG(canvas);
              // })
          }
        </script>
    </body>
</html>
```
