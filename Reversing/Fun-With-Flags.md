# Solution

## What is given

The python code that runs the shop, and a link to the system

## How-To

1. Buy Russia flag using 1st vulnerability
2. Make enough (1337) money to still be able to buy CSA flag
3. Sell all flags except Russia flag
4. Try to buy CSA flag (it will succed)
5. Display your flags to get the code

## Behind-The-Scenes

There are two vulnerabilities to consider:

### Making money

Making as-much-as-you-need money is possible due to a weakness in the loop that occurs in *sell_flag_menu()* flow: No reset of *flag_to_sell*!
The way to utilize this is to buy validly **X** flags,
Now try to sell **X** flags,
First, sell validly one flag (the most expensive btw..)
Second, insert invalid index as the next flag you want to sell

Whats going to happen is that *user.sell_flag* will be triggered, as the variable *flag_to_sell* is set to be the last one that was sold.

### Acquiring CSA flag

Now to get the CSA flag we need to note the following fact:

The string that displays user stats calculates the fraction between the user value and his colors/stripes/stars.

This calculation involves divison, so we look at the stats of the flags and we can see that Russia flags has 0 stars! This means that if Russia flag is the only flag you have, then trying to display your stats will raise an exception.

Finally, we need to see how this impacts the *buy_flag_menu()*- We have only Russia flag so as we've said *str(user)* will raise an exception, so we can easily see that chronologically:
1. *allowed_to_buy_flag* is set to *True* because first validation based only on amount of money
2. Then, there is *str(user)* before any other validation, so en exception is raised on the flow skips the DONT_BUY_CSA_FLAGS logic, so the purchase can be complete!


