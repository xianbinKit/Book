##### Question :

\[App\] if we're in the real pre-commit handler we can't actually add any new fences due

##### Solution :

in your Xcode:

* Click on your active scheme name right next to the Stop button
* Click on Edit Scheme....
* in Run \(Debug\) select the Arguments tab
* in Environment Variables click +
* add variable: OS\_ACTIVITY\_MODE and value: disable



