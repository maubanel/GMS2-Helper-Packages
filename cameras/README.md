![](../images/line3.png)

### Custom Cameras

<sub>[home](../README.md#user-content-gms2-packages---table-of-contents)</sub>

![](../images/line3.png)

I have included 5 custom cameras that extend the basic functionality found in **GameMaker**.

* `center_cam_create(player_id)`
* `center_lag_cam_create(player_id)`
* `zone_cam_create(player_id)`
* `zone_lag_cam_create(player_id)`
* `platformer_lag_cam_create((player_id))`

For most of these all you need to do is call the function and pass it the instance ID of the character you want the camera to follow and it should work. 

<br>

---

##### `Step 1.`\|`PCKGS`|:small_blue_diamond:

Download the [custom_cameras.yymps](../packages/custom_cameras.yymps) from this repository. Import the packge into the game you want to use it in and select **Tools | Import Local Package**. Press the <kbd>Add All</kbd> button then press the <kbd>Import</kbd> button.  This package comes with everything you need that includes 6 scripts and 5 objects.  You do not need to include any of these objects in the level calling the script is all you need to do.

![download custom_cameras.yymps](images/importPackage.png)

![](../images/line2.png)

##### `Step 2.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: 

The first camera is one that keeps the player dead center of the screen.  In any game where enemies come in from all directions this is a good choice. You only need to call it once though and these scripts should **NOT** be called from **Step** events.  I called the first camera in a **Other | Game Start** event that will run for the entire game.

`current_camera = center_cam_create(player_id, [clamp_cam])`

You need to pass it the instance of the player object you want the camera to follow.  In this case I can use `obj_player` as there is only a single instance of this character in the level. This function will create a camera and return the id if you want to further manipulate it.

![call center cam](images/CenterCam.png)

![](../images/line2.png)

##### `Step 3.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

When you press the <kbd>Play</kbd> button you will see that the camera keeps the player dead center the entire time.

https://user-images.githubusercontent.com/5504953/235547733-65725f97-91c8-4695-82ec-70e5c6282ee9.mp4

![](../images/line2.png)

##### `Step 4.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

`current_camera = center_cam_create(player_id, [clamp_cam])`

There is one optional parameter boolean `clamp_cam`.  It defaults to `true`.  This stops the camera from showing outside the playable area.  If set to `false` then it will follow the character right to the edge of the level.

https://user-images.githubusercontent.com/5504953/235547924-69589f72-ab46-4c8c-903f-45230b4a1a39.mp4

![](../images/line2.png)

##### `Step 5.`\|`PCKGS`| :small_orange_diamond:

The next camera is for games where we want to cheat the camera in front of the player and potentially add some elasticity to the camera (feels like it is on a spring or rubber band rather than on a stick).  

`center_lag_cam_create(player_id, [clamp_edges], [cam_distance], [max_cam_speed], [cam_lag])`

The only required parameter is the player_id for the character you would like to follow.  The default settings leads the camera to show 200 pixels in front of the player.

https://user-images.githubusercontent.com/5504953/235548144-5e57d602-2c34-467a-ad75-86f947ec4fbc.mp4

![](../images/line2.png)

##### `Step 6.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond:

`center_lag_cam_create(player_id, [clamp_edges], [cam_distance], [max_cam_speed], [cam_lag])`

`cam_distance` is the second optional parameter of the `center_lag_cam()` function.  It represents how many pixels in front of the player you want the camera to focus on.  The default is set to `200` pixels.  If you set it to `0` you will have the player centered but will get a more natural camera feel with the lab built in. This gives the player nose room to see more in front of the direction they are moving in.

https://user-images.githubusercontent.com/5504953/235548177-949c5e85-a85c-4c9f-9e70-b2605a157615.mp4

![](../images/line2.png)

##### `Step 7.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

`center_lag_cam_create(player_id, [clamp_edges], [cam_distance], [max_cam_speed], [cam_lag])`

The next parameter is `max_cam_speed`.  This is the fastest a camera can move in pixels per frame.  The lower the number the faster the camera will reposition.  For really twitchy games you want this to be small.  For a calm RPG you might want a slower camera so the number should be higher.

https://user-images.githubusercontent.com/5504953/235548161-86a1af20-6f05-441b-b42f-a506a83fa8c1.mp4

![](../images/line2.png)

##### `Step 8.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

`center_lag_cam_create(player_id, [clamp_edges], [cam_distance], [max_cam_speed], [cam_lag])`

The final parameter is `cam_lag` which is a scalar between `.01` and `1`.  This adds springiness to the camera as it gets lower.  A value of `1` will have no lag and a value of `.01` might have too much lag and if you player moves fast might move off screen.  Finding the right value is key here.

https://user-images.githubusercontent.com/5504953/235549534-a66d01e2-e579-467f-af24-6221a39efad0.mp4

![](../images/line2.png)

##### `Step 9.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

`zone_cam_create(player_id, [clamp_edges], [zone_left], [zone_right], [zone_top], [zone_bottom])`

The third camera is more like how the default camera behaves in **GameMaker** except we have a bit finer control on all four directions so we can have a more flexible dead zone.  This keeps the camera from moving as long as they are in the zone.  When the player moves out the camera moves to keep them on the edge of the zone.

https://user-images.githubusercontent.com/5504953/235649528-c7300a5d-14e5-46a1-a48b-6d39b03c12bf.mp4

![](../images/line2.png)

##### `Step 10.`\|`PCKGS`| :large_blue_diamond:

`zone_cam_create(player_id, [clamp_edges], [zone_left], [zone_right], [zone_top], [zone_bottom])`

The four parameters are how many pixels the camera can travel to the `zone_left` of center, `zone_right` of center, `zone_top` of center and `zone_bottom` of center.  I have drawn a representation of what the zone looks like based on the parameters below.

https://user-images.githubusercontent.com/5504953/235649562-2f0388ce-dcd8-49c9-9de8-d7b8d8d521ff.mp4

![](../images/line2.png)

##### `Step 11.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: 

`zone_lag_cam_create(player_id, [clamp_edges],[cam_lag], [zone_left], [zone_right], [zone_top], [zone_bottom])`

The fourth cam is the same as the zone cam above with addition of a spring on the camera with the `cam_lag` parameter which makes the movement a bit more natural with eases in and out when starting and stopping. The `cam_lag` should be kept between `.01` and `1`.

https://user-images.githubusercontent.com/5504953/235651235-e4ba836f-2947-4323-a115-1e66609eb852.mp4


##### `Step 12.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

`platformer_lag_cam_create(player_id, [clamp_edges],[cam_lag_h], [cam_lag_v], [zone_left], [zone_right])`

For a platformer we have a special camera that has camera lag and only adjusts the vertical position when the player is on the ground or going up in the air.  This creates a different feel that takes advantage of what a platformer might need to see ahead, and beneath the player while still keeping an interesting camera. There are 2 caveouts.  The player must be moving using `vspeed` and `hspeed` and not moving it on the x and y.  Since the camera is not moving when the player is not on the ground we need an `on_ground` boolean on the player object that tells the camera whether the player is on the ground or not. 

https://user-images.githubusercontent.com/5504953/235649601-4a3457f4-beb3-4341-aa56-7f395c5f681d.mp4

![](../images/line2.png)

##### `Step 13.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

https://user-images.githubusercontent.com/5504953/235547614-3bbc1f7b-fcbf-4edc-b668-2474ea8d7924.mp4


https://user-images.githubusercontent.com/5504953/235649649-951b3278-873f-4d25-b397-551d43484e23.mp4

https://user-images.githubusercontent.com/5504953/235649679-a206eb43-9489-4891-b339-8707dd9f96c2.mp4

![](../images/line2.png)

##### `Step 14.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 15.`\|`PCKGS`| :large_blue_diamond: :small_orange_diamond: 

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 16.`\|`PCKGS`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 17.`\|`PCKGS`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 18.`\|`PCKGS`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 19.`\|`PCKGS`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 20.`\|`PCKGS`| :large_blue_diamond: :large_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 21.`\|`PCKGS`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Package: Custom Cameras"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [home](../README.md#user-content-gms2-packages---table-of-contents)|
|---|
