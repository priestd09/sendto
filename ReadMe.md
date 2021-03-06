<h1><img src="https://avatars3.githubusercontent.com/u/16869703?v=3&s=32" height=32 width=32> Sendto</h1>

Sendto is a quick way for people to send you encrypted files and folders, without knowing anything about encryption, keys or passwords. This project was produced for Gopher Gala as a learning project. I am not a cryptographer, the code has not been audited (though it does use a reliable crypto library, it is possible there are vulnerabilities introduced by the usage), so please proceed at your own risk. I don't yet consider this project ready for production but would like to continue the experiment - contributions or suggestions are welcome. 

* No key generation or passwords. Sendto lets users use your PGP public key to encrypt files for you, and uploads them to the server encrypted for you to download. There is no difficult dance of sending keys or passwords on an insecure channel, or complex software for them to master. 
* Files encrypted at all times. Sendto cannot open your files because it only knows about your public key, so it can encrypt but never decrypt. TLS is also used for all connections. 
* Open Source. Sendto is completely open source, so that you can verify what happens to your files, and run it on your own server if you prefer self-hosting. Encryption uses the google library: golang.org/x/crypto/openpgp.

### Receive files securely

Just send people a link to your profile, and they can download an app for their platform to send you encrypted files. An example profile is here:

https://sendto.click/users/demo

This shows the public key, and a set of download links. Download the binary for your platform (or install from source if you prefer, see below), and then you can send a file to any sendto account for which you know the username, with a command like:

`sendto demo my/file/or/folder`

this will send the file to the demo account. You won't be able to download it though, as you need your own profile to access uploaded files. Please only send test files to the demo account. 

Once you've tried the demo, if you have a pgp key, or a keybase.io account, try setting up a user. The server can pull keys automatically from keybase.io so setup is easy. No email is required for sign up at this time. *You MUST use a PGP key*, not any other kind of key.

Once files are uploaded to your account, you're able to view and download them by logging in. Decryption happens on your machine, so that your private keys are never shared with the server. 


### Try it
https://sendto.click

### Open source on github
go get github.com/send-to

This app is open source so that you can build it yourself, and check what it does. If you have Go installed, you can also install the client and server from source with:

`go get github.com/send-to/sendto`

and then use the sendto command:

`sendto help` 

you can host the server yourself if you prefer to have complete control by checking out the server repo:

`go get github.com/send-to/sendtoserver`

### Created by
@kennygrant on twitter, <a href="https://github.com/kennygrant">github</a>, <a href="https://keybase.io/kennygrant">keybase.io</a>, <a href="https://sendto.click/users/kennygrant">sendto.click</a>. 
Contributions and pull requests welcome.

### Version History

##### Version 0.1
* Created for Gopher Gala 2016

##### Version 0.1.1
* Added warnings to readme, notes on possible bugs
* Fixed bug - if absolute paths given they should be truncated to the enclosing folder only for zip
* Added more specific warning on config failure

##### Version 0.1.2
* Add detailed errors for encryption/zip
* Complain if non-pgp key used

### Possible bugs and limitations

* Signatures are not yet checked, so no authenticity guarantee is given - we should instead sign if private keys are available locally, or consider tie-in with keybase.io.
* The sender username should be set by the user (ideally they should be prompted for it) - this ties in with signing above. 
* Would be nice to lean on keybase.io if possible more for authentication/getting keys - can be used as key server just now but is not the default - multiple key server support?
* Keys are cached locally for users (at ~/.sendto), so if you change your key you'd have to remove the prefs locally in order to update it. This needs fixed at some point obviously. 
* User enumeration is possible by numeric id, and there are no restrictions on who can send you files - neither is particularly desirable - perhaps consider using email as unique identifier and namespace for users?
* A few usability notes from Matthew - Readme should be updated, zip file for binaries should be named appropriately. 
* Times are shown in UTC - I rather like this but can see that others might prefer a local time.
