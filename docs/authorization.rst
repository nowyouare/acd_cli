Authorization
-------------

Before you can use the program, you will have to complete the OAuth procedure with Amazon.
The initially obtained OAuth credentials can subsequently be refreshed automatically when
necessary, which is at most once an hour.

It is necessary to have a (preferrably graphical) Web browser installed to complete the procedure.
You may use another computer for this than the one acd\_cli will run on eventually.

If you are a new user, your only option is to use the Appspot authentication method
which relays your OAuth tokens through a small Google Compute Engine app.
If you have a security profile which was whitelisted for Amazon Drive access (prior to fall 2016),
please skip to the Security Profile section.

Simple (Appspot)
++++++++++++++++

This authorization method was created to remove the initial barrier for most casual users. It will
forward your authentication data through an external computing platform service (Google App
Engine) and may be less secure than using your own security profile. Use it at your own risk.

You may view the source code of the Appspot app that is used to handle the server part
of the OAuth procedure at https://acd-api-oa.appspot.com/src.

You will not have to prepare anything to initiate this authorization method, just
run, for example, ``acd_cli init``.

A browser (tab) will open and you will be asked to log into your Amazon account
or grant access for 'acd-api'.
Signing in or clicking on 'Continue' will download a JSON file named ``oauth_data``, which must be
placed in the cache directory displayed on screen (e.g. ``/home/<USER>/.cache/acd_cli``).

Advanced Users (Security Profile)
+++++++++++++++++++++++++++++++++

You must have a security profile and have it whitelisted, as described in Amazon's
`ACD getting started guide
<https://developer.amazon.com/public/apis/experience/cloud-drive/content/getting-started>`_.
The security profile must be whitelisted for read and write aceess and have a redirect
URL set for ``http://localhost``.

Put your own security profile data in a file called ``client_data`` in the cache directory
and have it adhere to the following form.

.. code :: json

 {
     "CLIENT_ID": "amzn1.application-oa2-client.0123456789abcdef0123456789abcdef",
     "CLIENT_SECRET": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef"
 }

You may now run ``acd_cli -v init``.
The authentication procedure is similar to the one above. A browser (tab) will be
opened and you will be asked to log in. Unless you have a local webserver running on port 80,
you will be redirected to your browser's error page. Just copy the URL
(e.g. ``http://localhost/?code=AbCdEfGhIjKlMnOpQrSt&scope=clouddrive%3Aread_all+clouddrive%3Awrite``)
into the console.

Changing Authorization Methods
++++++++++++++++++++++++++++++

If you want to change between authorization methods, go to your cache path (it is stated in the
output of ``acd_cli -v init``) and delete the file ``oauth_data`` and, if it exists, ``client_data``.

Copying Credentials
+++++++++++++++++++

The same OAuth credentials may be used on multiple user accounts and multiple machines without a 
problem. To copy them, first look up acd\_cli's source and destination cache path like 
mentioned in the section above. Find the file/s ``oauth_data`` and possibly ``client_data`` in the
source path and just copy it/them to the destination path.

Accessing multiple Amazon accounts
++++++++++++++++++++++++++++++++++

It is possible to use the cache path environment variable to set up an additional cache that is 
linked to a different Amazon account by OAuth credentials. Please see the 
:doc:`setup section <setup>` on environment variables.

