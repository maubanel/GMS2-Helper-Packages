![](../images/line3.png)

### Screen Shake

<sub>[home](../README.md#user-content-gms2-packages---table-of-contents)</sub>

![](../images/line3.png)

This package has one script `screen_shake` and one object `obj_shake`. 

* Syntax:
`screen_shake()`

* Optional arguments:
* `_number_of_shakes`.  Default value is `10`.  This is how many time the camera changes postions for the shake.  It will make it looks like it shakes faster if the number is higher or lower is the number is lower.
* `_shake_range`. Default value is `10`. A radius of pixels for how far the camera will move.  This increased the amoutn of displacement of the shake.
* `_shake_length`.  Defautls to `0.5`.  This is the number of seconds the camera shakes before it stops.  
* `_angle_range`.  Defaults to `0.3`°.  This is how many degrees the camera tilts.  Be careful about making this larger than 2 as it will be very disorienting and cause dizinness.


<br>

---

##### `Step 1.`\|`PCKGS`|:small_blue_diamond:

Download the [screen shake](../packages/screen_shake.yymps) package.

![download screen_shake package](images/downloadPackage.png)

![](../images/line2.png)

##### `Step 2.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: 

This packages comes with multiple files.  You should have an **obj_shake** object and the following scripts:

* **cheap_perlin_noise**
* **get_active_camera**
* **scr_eases**
* **scr_noise_rng**
* **screen_shake**

There are mostly helper functions and you can do everything through the `screen_shake()` function.

![files with package](images/files.png)

![](../images/line2.png)

##### `Step 3.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

The simplest execution is to just call `screen_shake()` without passing any parameters. The shake will use the more expensive algorithm (looks better), will have a shake radius of 30 pixels, a shake rotation of 1°, a shake that will last for one second, with 5 octaves, harmonics of `0.3`, smooth transition between random points and a random seed of `0` . You can trigger it based on any event, I wired it up to a button press just to test the functionality by pressing the space bar. 

![call screen_shake](images/callScreenShake.png)

##### `Step 4.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Notice the screen shakes for a second. 

https://user-images.githubusercontent.com/5504953/235301006-c40e2b4d-4876-4d03-a0fd-ef04a382be1c.mp4

![](../images/line2.png)

##### `Step 5.`\|`PCKGS`| :small_orange_diamond:

`screen_shake(cheap, shake_amount, shake_rot_amount, shake_length, octave, harmonic, smooth, seed)`
We can customize the shake.  The first parameter is `cheap`.  This switches between a computational less expensive algorithm.  If set to false it just randomly picks a new position and moves to it at the frame_rate the game is set to. If you just need the *cheap* noise you can delete the `cheap_perlin_noise)()` and `scr_eases()` scripts.

If you keep it at the more expensive method it needs to be set a its default of `true`. This will allow you to quickly ease inbetween random points with tweening.  This allows for more realistic and smoother noise.

https://user-images.githubusercontent.com/5504953/235301013-a2aa0c9b-17ff-4f73-858c-a411cc73145b.mp4

![](../images/line2.png)

##### `Step 6.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond:

`screen_shake(cheap, shake_amount, shake_rot_amount, shake_length, octave, harmonic, smooth, seed)`
You can increase the intensity of the shake by displacing the camera by a greater amount.  It is set to a radius in pixles for the `shake_amount` parameter.  The larger the number the more the camera will shake. This example increases the `shake_amount` to `55` pixels.

https://user-images.githubusercontent.com/5504953/235301666-43839912-6d43-4d25-b2ed-9335caa72f7e.mp4

![](../images/line2.png)

##### `Step 7.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

`screen_shake(cheap, shake_amount, shake_rot_amount, shake_length, octave, harmonic, smooth, seed)`

The next parameter is `shake_rot_amount` which sets the rotation of the camera in degrees°.  This number should be kept small as it can be pretty disorienting and violent.  Use it cautiously.  The default is set to `1°`.

https://user-images.githubusercontent.com/5504953/235302262-e72df5a6-ad53-4c6e-b808-a92029e43457.mp4

![](../images/line2.png)

##### `Step 8.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

`screen_shake(cheap, shake_amount, shake_rot_amount, shake_length, octave, harmonic, smooth, seed)`

Now the `shake_length` which is the length in seconds and `octave` work together.  Please note that if you are using the cheap shake (`cheap` set to `true`) then `octave` will have no effect.  The longer the `shake_length` the more number of `octave` can be accomodated.  There is a function called `function num_of_octaves(total, octaves)` in which you pass the total amount of time in frames (seconds x room_speed) and the largest number of octaves you want and it returns the most amount of octaves possible. Each octave adds a set of points if there is room (needs to be at least one point between each random position to lerp through).

https://user-images.githubusercontent.com/5504953/235302236-68e20e43-bdeb-4820-939b-dcfb9f34048d.mp4

![](../images/line2.png)

##### `Step 9.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

`screen_shake(cheap, shake_amount, shake_rot_amount, shake_length, octave, harmonic, smooth, seed)`

The `harmonic` parameter is only for when we are using lerping when `cheap` is set to `false`.  It affects how much each octave effects the curve.  For a numnber greater than `1` it decreases the effect of each octave and for a setting of less than `1` it decreases it.  I would not exceed a range of `.1` to `2` but it is personal choice.

https://user-images.githubusercontent.com/5504953/235303002-3c01ee74-f6c2-47f5-996f-be84607f2a31.mp4

![](../images/line2.png)

##### `Step 10.`\|`PCKGS`| :large_blue_diamond:

`screen_shake(cheap, shake_amount, shake_rot_amount, shake_length, octave, harmonic, smooth, seed)`

The `smooth` parameter onlh works when `cheap` is set to `false`.  It smooths out the transitions between octaves.  So either it is a sudden change or a smoothed curve.

https://user-images.githubusercontent.com/5504953/235303018-38e4eeaa-16d0-4076-9ff0-018fdab9a495.mp4

![](../images/line2.png)

##### `Step 12.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

The final parameter of `seed` changes the random points in the curve. So if you don't like the way it shakes but all the other parameters are how you like it, change the seed until you find that right one!

https://user-images.githubusercontent.com/5504953/235303027-ae5c1e89-1c36-4140-b7fb-9aec5ae4cd72.mp4

![](../images/line2.png)

##### `Step 11.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: 

You can also download this sample project if you want to see it in action: [Screen Shake Sample](../sample-projects/ScreenShakeSample.zip). Press the <kbd>Tab</kbd> button to change rooms.

![sample project](images/sampleProject.png)

![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Package: Screen Shake"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [home](../README.md#user-content-gms2-packages---table-of-contents)|
|---|
