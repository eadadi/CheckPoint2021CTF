# Solution

## What is given

The code for a shopping assistant that includes:

1. main.c that handles the general flow of the system
2. shooping_cart.c/h implement interaction with items/cart

We are also given a coupon code that is:
```NOT_A_FLAG{I_4M_A_N3WB1E}```

## How-To

1. Apply the given coupon
2. Modify ```kilograms``` of item-1 to be a positive integer
3. Modify ```items``` of item-1 to be 0
4. Extract Flag-Number from shopping cart (by viewing it)

## Behind-The-Scenes

### Background

1. It can be observed that the *apply-coupon* method actually loads two coupons to the cart (and indeed after step 1 from above, the cart already has 2 items!)
2. This leads to guess that the flag is part of the second coupon memory
3. Observe that there are 2 bugs in *can-edit-item* method:
    - There is an assignment of the *item_type* to be a *TYPE_FRUIT* [Instead of a condition operator]
    - There is an assignment of the *item_type* to be a *TYPE_COUPON* [Instead of a condition operator]
4. Another observation is that the design of items in *shopping-cart* is as follows:
    - There is a wrapper-struct called *item*
    - Under it there are two properties:
        * type: can be either coupon or one of the existed products
        * product details, which implemented as a union type
5. Another observation is that the field that filteres visibility of the coupon when printing shopping-cart is *have_entered* from the *coupon_item* struct
6. The corollary from last 2 bullets is that *have_entered* is in the same memory location as *kilograms* field!!!

### Getting to the point

1. By applying the given coupon we are loading to the cart the second coupon (=> the flag) as the item with index 1
2. Then, By modifying the **kilograms** field of item-1 we implicitly set the visibility of the coupon to be ```true```
3. Now, the problem is that by editting an item we are falling to the bug from bullet 3.1 that sets our type to be a fruit
4. To avoid it, we also set **num-of-items** to be 0, so that we will fall to ***3.2*** bug!!!
5. This results in assignment of item-1 back to a coupon, so that printing to cart will give us the flag