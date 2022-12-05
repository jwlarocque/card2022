# Card 2022

![StableDiffusion-generated image](../Bitmaps/00297-2545456731-christmas%20star%20over%20Bethlehem%20by%20_moebius_.png)

### Centerline trace idea

* skeletonize (is this necessary?)
* select a random pixel
    * score each nearby pixel on proximity and direction (relative to vector to previous pixel(s))
        * for first pixel, select three? (i.e. also select "prev")
    * recurse one or more times - score is decaying(?) sum of best(?) child scores
        * also check curvature (derivative)?
        * exclude pixels which are already part of a path
    * append top scorer to the path
    * repeat with newly added pixel as the current pixel
    * if no nearby pixels or none meet a minimum score threshold, stop
        * might this exclude the final pixel which should've been added? (because it'll have no children)
    * return to the first pixel and travel in the opposite direction
* evaluate all pixel pairs and allow swaps (from path to path) if it would improve the total score
    * stop when no improvements can be made, or when a very small percentage of possible swaps in the last iteration were improvements
* delete orphan pixels and very short paths
* smooth (figure out how to do this...)

TODO:

* allow pixels to be in more than one path? (T and + intersections)
* create score lookup table (depending on window size there are a small number of possibilities)
* use points or tuples or something instead of passing x and y around everywhere
* break ties with random selection (instead of first)

Consider:

* just use the threshold/mask for starting pixels, and allow any to join the path? (score based on darkness)