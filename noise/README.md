![](../images/line3.png)

### Noise

<sub>[home](../README.md#user-content-gms2-packages---table-of-contents)</sub>

![](../images/line3.png)

Noise and random numbers are very valuable in video games. We will cover using noise as a random number ganerator.  This is based on this excellent [GDC talk](https://www.youtube.com/watch?v=LWFzPP8ZbdU). This allows us a bit more control over how we use and reuse random numbers. We also have a fast implementation of a take on value/perlin noise. 

<br>

---

##### `Step 1.`\|`PCKGS`|:small_blue_diamond:

Download the [noise](../packages/noise.yymps) package. Notice that you get three functions. It comes with a range of random noise functions in `scr_noise_rng`.  There is a a `cheap_perlin_noise()` function to create structured noise.  It used `scr_ease` to smooth out the transitions between points used by the cheap_perlin_noise function.

![download noise package](images/noise_functions.png)

![](../images/line2.png)

##### `Step 2.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: 

We can call `rng_var()` and if we pass no parameters then we will just get a random number that changes over time.  This function returns a real number between `0` and `1`. This example is picking a random y position using this noise function.  Notice that it is constantly changing and quite random. 

![rng_var()](images/rng_var.gif)

![](../images/line2.png)

##### `Step 3.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

`rng_var_norm()` is very similar except it returns a range from `-1` to `1`.

![rng_var_norm()](images/rng_var_norm.gif)

![](../images/line2.png)

##### `Step 4.`\|`PCKGS`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

`rng_var_range(start, end)` is very similar except it returns a range from the parameters passed `start` to `end`. For this to work the start value needs to be smaller than the end value. The below example is randomly selecting from `rng_var(-20, -10)` which is picking a fractional number between -20 and -10.

![rng_var_range(start, end)](images/rng_range.gif)

![](../images/line2.png)

##### `Step 5.`\|`PCKGS`| :small_orange_diamond:

`rng_var_val(value)` is very similar except it returns a real number range between `0` to `val` if val is positive and `val` to `0` if val is negative. The below example is randomly selecting from `rng_var(-15)` which is picking a fractional number between 0 and 15.

![rng_var_range(start, end)](images/rng_value.gif)

![](../images/line2.png)

##### `Step 6.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond:

This can become powerful as we can recall the same random number sequence at will to create more complex structures.  In the case below I am passing `rng_rand()`, `rng_rand_norm()`, `rng_rand_range()` and `rng_rand_val` the same seed.  So every frame it is picking the exact same `y` value and even though it is random, we are refering to the same index over and over again so the noise no longer moves like it did above.

![alt_texadd indexes into noise functiont](images/rng_indexes.gif)

![](../images/line2.png)

##### `Step 7.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

In the below example of noise you can see that if we just use noise and map it to the `y` axis we get random distribution and very chaotic transformation along the x axis.  It we use a smooth noise function like `cheap_perlin_noise()` we can get a more gradual transition.  

`cheap_perlin_noise(count, total, octaves, [seed], [smooth], [harmonic])`

The first parameter we pass is the current index into the  `count` parameter.  This should start at `0` and if you want it to tile horizontally needs end at a power of `2`.  For example 2, 4, 8, 16, 32, 64, 128, 256 etc...  This way the first value and last value of noise will be the same so it will tile perfectly.  If not then there would be a hitch if you loop back to the 0 count.  This value should be a whole number and not fractional.  

The second input are how many octaves.  With one octave there is a single point, the begining and the end.  If it is tiling then it will be a straigh line.  Adding an octive puts a point in the middle and split the line tino 2 allowing for another harmonic.  An octovae of 3 adds to more points spliting it into 4 line segments and an octave of 4 splits it to 8 segments and so on.  So we continue to add a point until we can no longer add points. This value should be a whole number and not fractional.  

The third parameter is optional and chnages the seed so it will randomly pick different points along the ocatves changing the shape of the curve.

The fourth parameter is to add smoothing (optional).  It defaults to `true`.  This makes the joints between lines curves to smoothly ease in and out of them.  If it is `false` you will get jagged sharp transitions.

The last value is `harmonic` and defaults to `.75`.  You can use a range between `.1` and `2`.  A value of `2` will reduce the influcence of every other octave by half of the prior.  So each octave creates a smaller delta.  This is nice when you want a fractal representation.  A value of `.1` will increase the amount of each octave's influence creating a more sudden transition.

https://user-images.githubusercontent.com/5504953/234905980-15dbd622-302a-438e-8b85-4abe0701f6a8.mp4


![](../images/line2.png)

##### `Step 8.`\|`PCKGS`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Here is an example of cheap perlin noise being used in practical ways. 

The first example is shifting the result of perlin noise from a range of `0` to `1` to a range of `-1` to `1`.  We do this by multiply the noise function by 2 (extending the range to 0 and 2) then subtracting 1 from it.  We then multiply it by a 100 to get a range of +- 100 pixlels on the y position of the ship.

The second example is adjusting the alpha to make it look like it is a broken light that is flashing eratically.  We pass the values `cheap_perlin_noise(i, 2048, 16, 4, true, .2)`.  We are getting values from `0` to `2048` ending on the same value so it loops seamlessly.  We have `16` harmonics, a random seed of `4` and smoothing between points.  We set the `harmonic` at `.2` to really accentuate the range as we want a large fluctation in this broken light.

The next example is a wheel that is turning eratically from one angle to another.  We use the noise function to affect the image_nalge and scale the range between `0` and `359`.

The blend function chnages the hue of an hsv value changing the hue of a light over time.

We then pass two separate noises with different seeds into the x and y scale of the circle allowing for hte scale to change in interesting ways.

![perlin noise examples](images/PerlinExamples.gif)

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

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Package: PACKAGE NAME"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [home](../README.md#user-content-gms2-packages---table-of-contents)|
|---|
