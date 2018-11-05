
MOCHA225 (ABND) [Oct 28th at 5:56 PM]
I can’t figure out why I’m not getting a compilation error on the pet app
I add sanity checks in Pet Provider and get 23 errors
package com.example.android.pets.data;
import android.content.ContentProvider;
import android.content.ContentUris;
import android.content.ContentValues;
Click to expand inline 175 lines


13 replies
Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) at line 146 you have an open {  and need to close it after the throw new IllegalArgument...  so in line 149

Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) also at line 138 the } bracket shouldn't be there. You can delete that

Jorge E. Covarrubias (ABND) [7 days ago]
the latter reason might would have thrown of your formatting creating a little bit of confusion.

MOCHA225 (ABND) [7 days ago]
That got me down to 14 errors.  And values became red

Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) What are the errors? do you have this up on github? That was from a quick visual scan

MOCHA225 (ABND) [7 days ago]
I’ll put on github.  Fixed all the errors but app stops and wants to be restarted.

MOCHA225 (ABND) [7 days ago]
here is my github link https://github.com/mocha225/mocha225pets.git
GitHub
mocha225/mocha225pets
Contribute to mocha225/mocha225pets development by creating an account on GitHub.
 

Jorge E. Covarrubias (ABND) [7 days ago]
i'm coming. was helping someone else. :grin:

Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) Here we go.
First clean up the empty space in your if statements in the PetProvider when doing the sanity checks. then at line 168, you need an open bracket { for your if statement and close it at line 170.
Hit CTRL + ALT + L to reformat your code and make it easier to read. You should notice the it will remove some indentation after line172.

Jorge E. Covarrubias (ABND) [7 days ago]
Now that that is set, I was getting an error in the catalogActivity that the cursor was null. "Attempt to invoke interface method 'void android.database.Cursor.close()' on a null object reference"

So this was telling me that it was empty. Why is it empty? I took a look at the cursor declaration in line 75 and saw that it points to PetEntry.CONTENT_URI located in the PetContract.

I noticed nn the PetContract, your String
public static final String CONTENT_AUTHORITY = ".com.example.android.pets"; shouldn't have that . before the com.

it should read
public static final String CONTENT_AUTHORITY = "com.example.android.pets";


Jorge E. Covarrubias (ABND) [7 days ago]
Since it couldn't locate the authority at .com.example.android.pets, the cursor is empty and that is why we were getting that error. After fixing that, the app was able to run on my emulator.


MOCHA225 (ABND) [7 days ago]
that you.  I’m getting ready for bed and will have to work on this tomorrow.  Have a good night.  Thanks.



MOCHA225 (ABND) [6 days ago]
Jorge you are the best!  It still amazes me how such little things make such havoc.  Have a great night.
