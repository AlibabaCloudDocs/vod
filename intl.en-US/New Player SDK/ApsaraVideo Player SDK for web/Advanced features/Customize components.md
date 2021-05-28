Customize components 
=========================================

ApsaraVideo Player V2.3.0 and later allow you to customize components. You can design logic and features, such as bullet messages and playlists on a node in a playback lifecycle. 

Lifecycle nodes 
------------------------------------

The following table describes the key methods that are used in ApsaraVideo Player. 


| Method or status |                                                           Description                                                           |
|------------------|---------------------------------------------------------------------------------------------------------------------------------|
| init             | Loads the initial configurations used to create an instance.                                                                    |
| createEl         | Creates the user interface (UI) of components. The parameter is the Div in the player container.                                |
| created          | Indicates that the player is created and the player API can be called.                                                          |
| ready            | Indicates that the video is ready for playback.                                                                                 |
| play             | Indicates that the player starts to play a video.                                                                               |
| pause            | Indicates that the player pauses a video.                                                                                       |
| playing          | Indicates that the player is playing a video.                                                                                   |
| waiting          | Indicates that the player is waiting for data.                                                                                  |
| timeupdate       | Indicates the changes to playback events. The playback time can be obtained by the timeStamp attribute of the second parameter. |
| error            | Indicates a playback error.                                                                                                     |
| ended            | Indicates that the playback ends.                                                                                               |
| dispose          | Destroys a player.                                                                                                              |



Implementation 
-----------------------------------

**Define a component** 

You can define a component by using one of the following methods:

* Call the Component method that is provided by ApsaraVideo Player

  




    var StaticADComponent = Aliplayer.Component({
        init:function(adAddress,toAddress)
        {
          this.adAddress = adAddress;
          this.toAddress = toAddress;
          this.$html = $(html);
        },
        createEl:function(el)
        {
          this.$html.find('.ad').attr('src',this.adAddress);
          var $adWrapper = this.$html.find('.ad-wrapper');
          $adWrapper.attr('href',this.toAddress);
          $adWrapper.click(function(){
            Aliplayer.util.stopPropagation();
          });
          this.$html.find('.close').click(function(){
            this.$html.hide();
          });
          $(el).append(this.$html);
        },
        ready:function(player,e)
        {
        },
        play:function(player,e)
        {
           this.$html.hide();
        },
        pause:function(player,e)
        {
           this.$html.show();
        }
    });



* **Use the class that is provided by JavaScript ES6**

  



**Note**

This method is recommended when your project is built in JavaScript ES6 by using webpack or babel.

    export default class StaticADComponent
    {
        constructor(adAddress,toAddress) {
          this.adAddress = adAddress;
          this.toAddress = toAddress;
          this.$html = $(html);
        }
    
        createEl(el)
        {
          this.$html.find('.ad').attr('src',this.adAddress);
          this.$html.attr('href',this.toAddress);
          let $adWrapper = this.$html.find('.ad-wrapper');
          $adWrapper.attr('href',this.toAddress);
          $adWrapper.click(()=>{
            Aliplayer.util.stopPropagation();
          });
          this.$html.find('.close').click(()=>{
            this.$html.hide();
          });
          $(el).append(this.$html);
        }
    
    
        ready(player,e)
        {
        }
    
        play(player,e)
        {
           this.$html.hide();
        }
    
        pause(player,e)
        {
           this.$html.show();
        }
    }





**Set the attributes of the defined component** 

After you define a component, you need to add the component to the configurations of the player so that the component can be used. The following table describes the attributes that you need to set for the component. 


| Attribute |                                    Description                                     |
|-----------|------------------------------------------------------------------------------------|
| name      | The name of the component. The player obtains the component by the component name. |
| type      | The type of the component.                                                         |
| args      | The parameters of the component.                                                   |



In the following code, all parameters are the initial parameters of a component. 

    var player = new Aliplayer({
        id: "J_prismPlayer",
         autoplay: true,
         isLive:false,
         playsinline:true,
         controlBarVisibility:"click",
         cover:"",
         components:[
         {name:'adComponent',type:StaticAdComponent,args:['http://cdnoss.youkouyang.com/cover.png']},
         notParameComponent,
         {name:'adComponent1',type:notParameComponent}
         ]                 
        });





**Obtain a component** 

You can call the getComponent method and set the name parameter to obtain a component 

    var component = player.getComponent('adComponent');





