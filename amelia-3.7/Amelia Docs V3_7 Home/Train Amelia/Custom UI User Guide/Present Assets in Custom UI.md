-   [CSP Headers for PDFs](#PresentAssetsinCustomUI-CSPHeadersforPDFs)
-   [Download and Preview Icons](#PresentAssetsinCustomUI-DownloadandPreviewIcons)
-   [Display Options](#PresentAssetsinCustomUI-DisplayOptions)
    -   [Previews](#PresentAssetsinCustomUI-Previews)
    -   [Overlays](#PresentAssetsinCustomUI-Overlays)
The custom user interface provides a series of options when video, documents, and other media when a BPN Present Task presents media within the conversation flow. 
# CSP Headers for PDFs
For PDF files to be previewed, the CSP headers should be updated then deployed with the UI Bundles editor in Amelia's administration pages. Add the resource `https://cdnjs.cloudflare.com` as either the `default-src` or `script-src`. And `blob:` should be added to `connect-src`.
``` groovy
default-src 'self' 'unsafe-eval' 'unsafe-inline' fonts.googleapis.com https://cdnjs.cloudflare.com *.youtube.com *.vimeo.com *.archive.org fonts.gstatic.com maps.googleapis.com data: blob:; connect-src 'self' blob: ws:; img-src 'self' maps.googleapis.com data: blob:;
```
# Download and Preview Icons
Small icons are used to download assets or preview assets. Click the download icon to open a file explorer popup. Click the preview icon to open the document in an overlay that hides the custom user interface. Click the X link at the top right of the overlay to return to the conversation space.
![](attachments/20809368/20809372.jpg)
Figure. Download and Preview Icons
# Display Options
Video, image, and document assets can be presented different ways.
-   With or without file name and file size asset details
-   With or without one or both icons to download and preview assets
-   With or without a preview thumbnail image
Assets rendered without a preview thumbnail image display instead in a small bubble with a download icon and file name. Click the bubble to open a file explorer popup.
Display options are set with the Properties panel for a BPN Present task in the Process Knowledge workspace.
![](attachments/20809368/20809399.png)
Figure. BPN Present Task Properties Panel
## Previews
Clicking any preview thumbnail opens an overlay with the full-sized asset, for example, to play a video asset.
Images and document previews are rendered as single image without file details or a card with the preview image above and file details below. For video previews, only the first frame displays and the video cannot play in preview mode.
Multi-page PDF and HTML assets cannot be scrolled when in preview within a conversation. Click the preview to display an overlay and scroll.
![](attachments/20809368/20809405.png)
Figure. Sample Previews for Images, Video, and No Preview
## Overlays
The overlay to display the full sized asset differs visually based on the web browser.
-   The video overlay includes controls to play, stop, pause, go back, and go forward
-   PDF assets display in an overlay with scroll, zoom in, zoom out, fit to page, and other options. The PDF overlay also disables the download option in the Chrome, Safari, and IE browsers but enabled in the Firefox browser.
-   HTML displayed in an overlay is the same as video or PDF. However, links do not work in overlay. And the overlay appears in a separate browser window on top of the parent window instead of a full window overlay panel.
![](attachments/20809368/20809396.png)
Figure. Sample Image Overlay
![](attachments/20809368/20809401.png)
Figure. Sample Video Overlay
![](attachments/20809368/20809403.png)
Figure. Sample PDF Overlay in Firefox Browser
## Attachments:
![](images/icons/bullet_blue.gif) [amelia_v3_customui_present_icons_3.7.x.jpg](attachments/20809368/20809372.jpg) (image/jpeg)  
![](images/icons/bullet_blue.gif) [image2019-7-19_9-54-58.png](attachments/20809368/20809396.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_9-58-17.png](attachments/20809368/20809397.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_9-59-51.png](attachments/20809368/20809398.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_10-1-44.png](attachments/20809368/20809399.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_10-16-43.png](attachments/20809368/20809401.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_10-17-14.png](attachments/20809368/20809402.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_10-18-35.png](attachments/20809368/20809403.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2019-7-19_10-31-8.png](attachments/20809368/20809405.png) (image/png)  
