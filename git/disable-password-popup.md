### Disable GUI Git Password Popup

In gnome, it seems like if you have GIT_ASKPASS / SSH_ASKPASS 
env variables set then git will automatically use that to query for user password.

This can be somewhat irritating. To work around this issue, try running:
```
unset SSH_ASKPASS
unset GIT_ASKPASS
```

If you only want to disable the query for password in git. You can also set the core.askpass settings:
```
git config --global core.askpass ""
```

[source](http://stackoverflow.com/questions/21422782/prevent-git-from-popping-up-gnome-password-box)

