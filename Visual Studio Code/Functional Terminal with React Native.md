Up until at least 2021, VS Code's terminal would not function for me when coding with React Native. This was an issue for my Mobile Application Development class in Macquarie University. Fortunately, a tutor whom I never met found a solution and shared it in an FAQ document on the class' online forum. Basically, it has to do with the Windows' policy of running scripts. The solution is as follows.    

Run Powershell as Administrator:

1. Enter: Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

Another option is to use "Unsigned" instead of "RemoteSigned", which should be the least restrictive option but is likely to introduce security concerns.

As the default ExecutionPolicy is Restricted, the change can be reversed with:

1. Set-ExecutionPolicy Restricted -Scope CurrentUser