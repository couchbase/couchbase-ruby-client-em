# EXAMPLE

Like any Deferrable eventmachine-based protocol implementation, using EM-Couchbase involves making calls and passing blocks that serve as callbacks when the call returns.

    require 'em-couchbase'

    EM.run do
      couchbase = EM::Protocols::Couchbase.connect
      couchbase.set "a", "foo" do |response|
        if response.success?
          couchbase.get "a" do |response|
            puts response.inspect
          end
        end
      end
      couchbase.incr "bar", :initial => 100500 do |response|
        if response.success?
          couchbase.get "bar" do |response|
            puts response.inspect
            EM.stop
          end
        end
      end
    end

## SUPPORT

If you found an issue, please file it in our [JIRA][1]. Also you are
always welcome on `#libcouchbase` channel at [freenode.net IRC servers][2].

Documentation: [http://rdoc.info/gems/couchbase-em][3]

[1]: http://couchbase.com/issues/browse/RCBCEM
[2]: http://freenode.net/irc_servers.shtml
[3]: http://rdoc.info/gems/couchbase-em
