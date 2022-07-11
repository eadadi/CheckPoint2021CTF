# Solution

## What is given

The code for a shopping assistant that includes:

1. main.c that handles the general flow of the system
2. shooping_cart.c/h implement interaction with items/cart

## Idea

A linear time brute-force utilizing types problem in the code

## How-To

1. Load the coupuns by option 5 in the store
2. Then, Modify the length of the coupun (Remark 1) to be the current known length of the FLAG + 1
3. Now, again by option 5 in the store (apply coupun) brute-force through all posibilities  to the next character of Flag
4. After discovering next char, load the coupon again to be able to guess next char (Remark 2)
5. Repeat untill getting the FLAG

Remark 1: As in the first Computed-Shopping-Assistant, the `shopping-cart` item is being used simultanously as a coupon item and as a grocerry item. This enables editing some of the coupon features, and it can be seen on the code that the attribute 'amount_loaves' happen to be the same as the length of a coupon.

Remark 2: Just as last time, we remove that item, then we add arbitrary product (fruit) to the cart, then we modify the number of items to be zero, and then just by trying to edit this product again we convert it to a coupon
