Configure the skinLayout attribute 
=======================================================

This topic describes the skinLayout attribute, the rules for configuring the skinLayout attribute, and how to configure attributes to customize components. 

skinLayout attribute 
-----------------------------------------

ApsaraVideo Player allows you to use the skinLayout attribute to specify whether to display the following three types of components and specify the display area of each component. 

* Buttons for playback

  

* Loading animation components

  

* User interface (UI) components of the control bar

  




You can modify the skinLayout attribute by configuring the aliplayer-min.css file of the player. For more information, see [Configure the player skin]().

Rules for configuring the skinLayout attribute 
-------------------------------------------------------------------

* If you do not set the skinLayout attribute, all the components are displayed by default.

  

* If you set the skinLayout attribute to an empty array or false, all components are hidden.

  

* You can configure only three UI components in the children attribute of the control bar for live steaming. The three UI components are liveDisplay, fullScreenButton, and volume.

  




Configure attributes to customize components 
-----------------------------------------------------------------

The align attribute specifies the alignment method of the child component relative to the parent component.

* `'cc'`: indicates absolute centering relative to the parent component.

  

* `'tl'`: indicates alignment in the upper-left corner relative to the parent component. The child component is affected by the location of peer components and takes the upper-left corner of a peer component as the offset origin. This method is similar to the `float: left` setting in a CSS file.

  

* `'tr'`: indicates alignment in the upper-right corner relative to the parent component. The child component is affected by the location of peer components and takes the upper-right corner of a peer component as the offset origin. This method is similar to the `float: right` setting in a CSS file.

  

* `'tlabs'`: indicates absolute alignment in the upper-left corner relative to the parent component. The child component is not affected by the location of peer components and takes the upper-left corner of the parent component as the offset origin.

  

* `'trabs'`: indicates absolute alignment in the upper-right corner relative to the parent component. The child component is not affected by the location of peer components and takes the upper-right corner of the parent component as the offset origin.

  

* `'blabs'`: indicates absolute alignment in the lower-left relative to the parent component. The child component is not affected by the location of peer components and takes the lower-left of the parent component as the offset origin.

  

* `'brabs'`: indicates absolute alignment in the lower-right relative to the parent component. The child component is not affected by the location of peer components and takes the lower-right of the parent component as the offset origin.

  




The x and y attributes specify the position of a child component with the location of the parent component as the offset origin.

* x: a parameter of the number type. The x attribute specifies the offset in the horizontal direction. For more information about the offset origin, see the description of the `align` attribute. This attribute is invalid if the align attribute is set to `cc`.

  

* y: a parameter of the number type. The y attribute specifies the offset in the vertical direction. For more information about the offset origin, see the description of the `align` attribute. This attribute is invalid if the align attribute is set to `cc`.

  




Default settings of the skinLayout attribute in ApsaraVideo VOD 
------------------------------------------------------------------------------------

**Default settings for the HTML5 player of ApsaraVideo VOD** 

    skinLayout:[
       {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {
          name: "H5Loading", align: "cc"
        },
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay"},
        {name:"tooltip", align:"blabs",x: 0, y: 56},
        {name: "thumbnail"},
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
            {name: "progress", align: "blabs", x: 0, y: 44},
            {name: "playButton", align: "tl", x: 15, y: 12},
            {name: "timeDisplay", align: "tl", x: 10, y: 7},
            {name: "fullScreenButton", align: "tr", x: 10, y: 12},
            {name:"subtitle", align:"tr",x:15, y:12},
            {name:"setting", align:"tr",x:15, y:12},
            {name: "volume", align: "tr", x: 5, y: 10}
          ]
        }
      ]



**Default settings for the Flash player of ApsaraVideo VOD** 

    skinLayout:[
        {name:"bigPlayButton", align:"blabs", x:30, y:80},
        {
          name:"controlBar", align:"blabs", x:0, y:0,
          children: [
            {name:"progress", align:"tlabs", x: 0, y:0},
            {name:"playButton", align:"tl", x:15, y:26},
            {name:"nextButton", align:"tl", x:10, y:26},
            {name:"timeDisplay", align:"tl", x:10, y:24},
            {name:"fullScreenButton", align:"tr", x:10, y:25},
            {name:"streamButton", align:"tr", x:10, y:23},
            {name:"volume", align:"tr", x:10, y:25}
          ]
        },
        {
          name:"fullControlBar", align:"tlabs", x:0, y:0,
          children: [
            {name:"fullTitle", align:"tl", x:25, y:6},
            {name:"fullNormalScreenButton", align:"tr", x:24, y:13},
            {name:"fullTimeDisplay", align:"tr", x:10, y:12},
            {name:"fullZoom", align:"cc"}
          ]
        }
    ]



**Effect** ![Default settings of the skinLayout attribute in ApsaraVideo VOD](../images/p270003.png)

Default settings of the skinLayout attribute in ApsaraVideo Live 
-------------------------------------------------------------------------------------

**Default settings for the HTML5 player of ApsaraVideo Live** 

    skinLayout: [
        {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay", align: "cc"},
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
              {name:"liveDisplay", align:"tlabs", x: 15, y:6},
              {name:"fullScreenButton", align:"tr", x:10, y: 10},
              {name:"subtitle", align:"tr",x:15, y:12},
              {name:"setting", align:"tr",x:15, y:12},
              {name:"volume", align:"tr", x:5, y:10}
            ]
        }
      ]



**Default settings for the Flash player of ApsaraVideo Live** 

    skinLayout: [
        {name: "bigPlayButton", align: "blabs", x: 30, y: 80},
        {name: "errorDisplay", align: "tlabs", x: 0, y: 0},
        {name: "infoDisplay", align: "cc"},
        {
          name: "controlBar", align: "blabs", x: 0, y: 0,
          children: [
              {name:"liveDisplay", align:"tlabs", x: 15, y:25},
              {name:"fullScreenButton", align:"tr",  x:10, y:25},
              {name:"volume", align:"tr",  x:10, y:25}
            ]
        }
      ]



**Effect** ![Default settings of the skinLayout attribute in ApsaraVideo Live](../images/p270004.png)
