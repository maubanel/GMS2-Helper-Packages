![](../images/line3.png)

### Bouncing Ball

<sub>[home](../README.md#user-content-gms2-packages---table-of-contents)</sub>

![](../images/line3.png)

This package has 4 scripts.  You only need to call two of them and the other two are called by the scripts themself.

* Syntax::
`ball_bounce_simple(_parent_obj, _bounce_off_bounds=true)`

* Arguments:
* `_parent_obj` game needs to pass a single reference for all bouncing balls.  If there is one ball boject you would pass tis object otherwise use a common parent object on all balls.

* Optional Arguments:
* `_bounce_off_bounds` defaults to True. Determines whether balls bounces off edges of level to say in bounds.

* Description:
The script `ball_bounce_simple` requires the object passed to be circular (the collision detection is done within this function and only works properly with circles) and must contain a variable called `radius` which holds the radius of the circle.  The origin needs to be in the middle of the circle.  This simple collision treats all balls as the same mass.

* Syntax::
`ball_bounce(_parent_obj, _bounce_off_bounds=true)`

* Arguments:
* `_parent_obj` game needs to pass a single reference for all bouncing balls.  If there is one ball boject you would pass tis object otherwise use a common parent object on all balls.

* Optional Arguments:
* `_bounce_off_bounds` defaults to True. Determines whether balls bounces off edges of level to say in bounds.

* Description:
The script `ball_bounce` requires the object passed to be circular (the collision detection is done within this function and only works properly with circles) and must contain a variable called `radius` which holds the radius of the circle.  The origin needs to be in the middle of the circle.  Each object needs a variable called `mass` which holds the weight of the object.  The scale is arbitrary and the mass is realtive (so an object with a mass of `4` is twice as heavy as a mass of `2`).  You also need to include a variable called `restitution`.  If it is set to `1` it is a perfectly elastic collision so no energy is lossed by the bound.  Any value greater will accelerate the bounce and smaller will lose enery after each bounce.

<br>

---

##### `Step 1.`\|`PCKGS`|:small_blue_diamond:

Download the [ball bounce](../packages/scr_ball_bounce.yymps) package of scripts. Import the package per the instructions in the home page of this GitHub repository.

![download screen_shake package](images/downloadPackage.png)

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 2.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: 

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 3.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 4.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 5.`\|`PCKGS`| :small_orange_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 6.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 7.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 8.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 9.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 10.`\|`PCKGS`| :large_blue_diamond:

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 11.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: 

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 12.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

![alt_text](images/.png)

![](../images/line2.png)

##### `Step 13.`\|`PCKGS`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

![alt_text](images/.png)

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

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Package: Ball Bounce"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [home](../README.md#user-content-gms2-packages---table-of-contents)|
|---|
