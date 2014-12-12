===================
Facebook Python SDK
===================

This client library is designed to support the `Facebook Graph API`_ and the
official `Facebook JavaScript SDK`_, which is the canonical way to implement
Facebook authentication. You can read more about the Graph API by accessing its
`official documentation`_.

.. _Facebook Graph API: https://developers.facebook.com/docs/reference/api/
.. _Facebook JavaScript SDK: https://developers.facebook.com/docs/reference/javascript/
.. _official documentation: https://developers.facebook.com/docs/reference/api/

Basic usage:

::

    graph = facebook.GraphAPI(oauth_access_token)
    profile = graph.get_object("me")
    friends = graph.get_connections("me", "friends")
    graph.put_object("me", "feed", message="I am writing on my wall!")

Media Uploads:

We added video posting support and instead of having two separate methods which were nearly identical, besides the post url, 
it was decided to turn it into one simple method. Note the second last parameter is a boolean telling us what type of media(image or not) is being uploaded. 
Images and videos are the only mediums currently supported.

::

    For photo uploads:

    kwargs = {'title':'testing', 'description':'just a test'}
    graph = facebook.GraphAPI(oauth_access_token)
    graph.put_media(os.path.join(os.getcwd(), '<sample_photo>.jpg'), None, True, **kwargs)


    For video uploads:

    kwargs = {'title':'testing', 'description':'just a test'}
    graph = facebook.GraphAPI(oauth_access_token)
    graph.put_media(os.path.join(os.getcwd(), 'sample_video.mp4'), None, False, **kwargs)


If you are using the module within a web application with the JavaScript SDK,
you can also use the module to use Facebook for login, parsing the cookie set
by the JavaScript SDK for logged in users. For example, in Google AppEngine,
you could get the profile of the logged in user with:

::

    user = facebook.get_user_from_cookie(self.request.cookies, key, secret)
    if user:
        graph = facebook.GraphAPI(user["access_token"])
        profile = graph.get_object("me")
        friends = graph.get_connections("me", "friends")


You can see a full AppEngine example application in examples/appengine.

Issues
======

This version of the facebook-sdk is provided as is. Bugs with the Graph API should be filed on `Facebook's
bugtracker`_.

.. _Facebook's bugtracker: https://developers.facebook.com/bugs/


Support & Discussion
====================

Documentation is available at https://facebook-sdk.readthedocs.org/en/latest/.

Have a question? Need help? Visit the library's `Google Group`_.

.. _Google Group: https://groups.google.com/group/pythonforfacebook
