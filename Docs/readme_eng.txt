What allows at the moment:
automatically create timings to the video and some of the above described chips :).

How to use:
1) Run VideoSubFinder.exe

2) In the menu select File-> Open Video, select the video file in which
   it is necessary to find sabies (avi, mpeg, mpg, asf, asx, wmv, ...)
   A video of the current video will appear in the Video Box.

3) You can immediately press Run (by default at the moment you must be in
   the Search tab), only the current time will be displayed in the Video Box
   processed frame (with a frequency of 1 times per second), if at the moment
   will be found at least one sub, then its image will be displayed in Image
   Box, the search results are dropped into the RGBImages folders (the original screens from
   video) and ISAImages (Intersected Subtitles Areas (by multiframe usage)), make sure that
   you had at least 100 mb of free disk space.

4) You can set the start and end time of the search for sabs, for this use
   key keys ctrl + z and ctrl + x (or through the menu Edit -> ...)
   Use the slider in the Video Box to navigate through the video :),
   for frame-by-frame navigation on video (use the arrows <-, ->, Up, Down
   or mouse wheel).

5) You can reduce the detection area by moving the vertical and horizontal
   Separating lines in the VideoBox with the mouse.

5) You can check the partially current settings:
   go to the Settings tab, move to any frame of the video (where available
   or there is no text), press the Test key (if there is text on the frame,
   Image Box should appear not an empty image processing result, otherwise
   black screen (but not necessary)) If the result of image processing with
   text is empty then it makes sense to loosen the settings (namely, most likely it will be
   it is enough to reduce Sum Color Difference and Sum Multiple Color Difference both
   on 600 or 500 or 400). The result of pressing the Test button is three
   After After Filtration, After Second Filtration, VEdgesPointsImage
   they can be viewed by clicking the buttons in the left and in the right above the Test button,
   and also in the TSTImages folder.
   
   "After First Filtration" is the resulting image as a result
   initial processing of the frame, the result of the processing is affected by all the "Settings for
   Operators Sobel "except one H-Vertical Threshold, all" Settings For
   Color Filter "except for one Sum Multiple Color Diff.
   
   "After Second Filtration" is the resulting image as a result
   secondary image processing (processing applied to the image
   resulting from "After First Filtration"), the result of processing
   affect all the "Settings for Linear Filtering", all "Settings for Points
   Color Borders ", all" Settings for Color Filter "except one
   Sum Color Diff.
 
   "VEdgesPointsImage" is translated as an image obtained from points
   vertical color boundaries. This image is obtained by converting
   frame into a black and white image, then applying a horizontal
   operator Sobel to determine the strength of the color difference. Then by threshold
   Filtering (all points whose strength is lower than the threshold set in the settings
   "H-Vertical Threshold" is replaced with black or white). These images
   Are used when checking whether adjacent frames with identical text or
   no)


6) At the end of the search for the sub it is desirable to go to the folder RGBImages and delete all
   those frames that are dummy, then on these images you can
   create an empty sub with timings, go to the OCR tab and click
   on Create Empty Sub, and there is the possibility of extending the sub by
   setting the "Min Sub Duration" value of the minimum duration of the sub
   seconds, and a logical attempt will be made to extend the sub
   by changing the time it ends.

More about settings:

Moderate Threshold - by means of complex operators from the source frame (when
   use of primary processing) the result is an image where
   Each point of the original frame is correlated with its strength (the strength of the color difference),
   and averaged so that in the region of the bright text and the pale text of force
   the color difference will not be too much different. Then on this
   image is the maximum strength of the color difference, this value
   multiplied by "Moderate Threshold", all points of power below the received
   The quantities are replaced by black or white.

H-Vertical Threshold - described in step 5 of "VEdgesPointsImage".

Line Height - used in algorithms to reduce the detection area, as well as
   linear filtration. The whole image is divided into horizontal lines
   thickness (height) "Line Height". Then each of these lines is analyzed in
   isolation.

Between Text Distance - is used for secondary image processing. How are you
   already had to understand the result of the primary processing, we get a binary
   image (speaking in simpler words consisting of points with only two
   possible colors black and white). This image is broken
   On the thickness line "Line Height". In each of these lines, blocks are searched for
   (presumably textual), by the principle if in the next column of height
   "Line Height" is at least one white point then the block has not yet ended. Then
   It looks like the distance between all the blocks found, it should not exceed
   The width of the video frame is multiplied by "Between Text Distance". If more then
   The block whose center is farthest from the center of the frame is deleted.

Text Center Offset-as a result of the above-described "From Text Distance"
   in each line there remains some possibly zero number of blocks. For these
   blocks (presumably a text string) is their center. If
   center is offset by more than "Text Center Offset" * ("video frame width" / 2) from
   center of the frame, then the block is removed most shifted from the center and so on until
   until the condition is satisfied. An important point is still what is being checked
   the location of the blocks in both halves of the image, otherwise all the blocks are deleted.

Min Points Number - in all remaining blocks in the line (read above)
   the number of white dots is counted if their number is less than the "Min Points Number" then
   all blocks in the line are deleted.

Min Points Density - the total area of ​​the remaining blocks in the row is counted
   (= SS) (read above), as well as the total number of white points in them (= S).
   It is checked that S / SS> = "Min Points Density", if not all of these
   blocks are deleted.

Segment Width - used in algorithms to reduce the detection area, and
   also in color filtration in secondary processing. Each line is divided into
   blocks of equal length "Segment Width" (not to be confused with those described above).

Min Segments Count - used in algorithms to reduce the detection area,
   as well as in color filtration in secondary processing. Minimum number
   neighboring blocks with sufficiently high color gradients at which
   The line containing them remains (will) be considered a supposedly textual
   (text-containing).

Sum Color Difference - used at the very beginning of the initial processing for
   reducing the detection area. The original video frame is split on the line
   thickness 1, each line is divided into blocks of equal width "Segment Width".
   In each block, the total color difference of neighboring points is calculated, if
   in the line are "Min Segments Count" of neighboring blocks with "swings"> = "Sum
   Color Difference ", then the line is assumed to be text-containing.

Min Sum Multiple Color Diff - used at the end of the secondary processing. How are you
   should still remember at the end of the secondary processing we possibly have in any of the
   line "Line Height" still left some blocks
   (potentially text-containing blocks). The whole area from their beginning to the end
   is divided into blocks of width "Segment Width". In each line (such lines
   will be "Line Height") of each such block is calculated by the
   differential. If in each line of any block of the "difference"> = "Sum Multiple
   Color Diff ", then such a block is considered potentially text containing.
   If as a result in this area there are "Min Segments Count" of such
   neighboring blocks, then the entire line is assumed to be text-based.

OCR Settings

Clear Images Logical (Remove Garbage) - performe cleaned image analyzes on present symbols and garbage.
	In case of turned off it will not try to remove potential garbage on cleaned images,
	sometimes this produce better results.

Sub Frames Length - the minimum duration of the sub.

Sub Square Error - in fact, the first detection of the sub goes as follows,
   found the first frame potentially containing the text, then if not less than "Sub
   Frames Length "including its frames are also potentially
   text-containing and the area of ​​their potentially text-based areas does not differ
   more than on "Sub Square Error" it is considered that the sub is found (further there is a test
   for the presence of the text string, if the test did not fail, then the search for the end of the sub is going on,
   matching identical sabs).

VEdgesPoints line error - used for stitching sabas, as well as detecting
   end of the sub. Neighboring frames are compared by the area of ​​points of vertical
   color boundaries in potentially text areas. If the areas differ
   no more than "VEdgesPoints line error" then it is considered that the end of the sub is not yet
   found.

Text Procent - used in the test for the presence of a text string. Looking for at least
   one line of thickness "Line Height" in which the sum of all lengths potentially
   text blocks in relation to the extent of the area on which they are
   are located> = "Text Procent". Also checks that this amount should be> =
   "Min Text Length" * "Video frame width".

Note:
A long search time is due to the fact that text detection is used
very complex and time-consuming algorithms developed by the Chinese (whose articles I
studied and implemented in this program), namely, the main used
(studied) works:

1) "A NEW APPROACH FOR FOR VIDEO TEXT DETECTION"
   Min Cai, Jiqiang Song, and Michael R. Lyu,
   Department of Computer Science & Engineering
   The Chinese University of Hong Kong Hong Kong SAR, China

2) Automatic Image Segmentation by Integrating Color-Edge Extraction
   and Seeded Region Growing 2001.
   Jianping Fan, David. K. Y. Yau, Member, IEEE, Ahmed. K. Elmagarmid,
   Senior Member, IEEE, and Walid G. Aref, Member, IEEE
 
3) Automatic Location of Text in Video Frames.
   Xian-Sheng Hua, Xiang-Rong Chen, Liu Wenyin, Hong-Jiang Zhang
   Microsoft Research China

4) EFFICIENT VIDEO TEXT RECOGNITION USING MULTIPLE FRAME INTEGRATION
   Xian-Sheng Hua, Pei Yin, Hong-Jiang Zhang
   Microsoft Research Asia, Dept. of Computer Science and Technology,
   Tsinghua Univ.

Also, the principle invented by Shalcker was partially used to
Reduce the video processing area on each frame.

In the first place, I first invented and implemented multi-frame
processing and linear filtering of processed frames, as well as some
improvement and modification of algorithms from the above listed works and their
implementation.