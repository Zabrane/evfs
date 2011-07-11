evfs: Erlang Virtual Filesystem
===============================

This application allows to create virtual filesystems on top of standard
`file` API. Imagine if you can do this:

    > {ok, Bin} = file:read_file("http://www.google.com/").

Or this:

    > {ok, Bin} = file:read_file("config://host").

Looks interesting, right? Now, basically, because of the way evfs operates,
you can feed unsuspecting Erlang code file names that are served off your VFSes. 
That's where the fun begins. (By the way, there's already some limited support 
for HTTP, just register `evfs_httpc_handler`: `evfs:register(evfs_httpc_handler, default)`).

Also, the way evfs is organized, you are not limited to this "scheme" way of overriding the
filesystem. You can override particular files, for example, or whole directories -- or
do that basing on some external state. So, for example, if some application expects a 
file at a hard coded location, just override it with your VFS.


You can register any number of virtual FS handlers using `evfs:register/2` function.
Also, by default, you get the handler that redirects file:// and plain filename requests
to the original file server, but you can unregiser it with `evfs:unregister/1` if you need.

Please bear in mind that this is a very early prototype. 

For an example on how to build a VFS, look into `test/evfs_test_fs.erl`. Hopefully
it will help.