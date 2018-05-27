[![Build Status](https://travis-ci.org/dmanto/Mojolicious-Plugin-Cron.svg?branch=master)](https://travis-ci.org/dmanto/Mojolicious-Plugin-Cron) [![Build Status](https://img.shields.io/appveyor/ci/dmanto/Mojolicious-Plugin-Cron/master.svg?logo=appveyor)](https://ci.appveyor.com/project/dmanto/Mojolicious-Plugin-Cron/branch/master)
# NAME

Mojolicious::Plugin::Cron - a Cron-like helper for Mojolicious and Mojolicious::Lite projects

# SYNOPSIS

    # Execute some job every 5 minutes, from 9 to 5

    # Mojolicious::Lite

    plugin Cron( '*/5 9-17 * * *' => sub {
        # do someting non-blocking but useful
    });

    # Mojolicious

    $self->plugin(Cron => '*/5 9-17 * * *' => sub {
        # same here
    });

\# More than one schedule, or more options requires extended syntax

    plugin Cron => (
    sched1 => {
      base    => 'utc', # not needed for local base
      crontab => '*/10 15 * * *', # every 10 minutes starting at minute 15, every hour
      code    => sub {
        # job 1 here
      }
    },
    sched2 => {
      crontab => '*/15 15 * * *', # every 15 minutes starting at minute 15, every hour
      code    => sub {
        # job 2 here
      }
    });

# DESCRIPTION

[Mojolicious::Plugin::Cron](https://metacpan.org/pod/Mojolicious::Plugin::Cron) is a [Mojolicious](https://metacpan.org/pod/Mojolicious) plugin that allows to schedule tasks
 directly from inside a Mojolicious application.
You should not consider it as a \*nix cron replacement, but as a method to make a proof of
concept of a project.

# BASICS

When using preforked servers (as applications running with hypnotoad), some coordination
is needed so jobs are not executed several times.
[Mojolicious::Plugin::Cron](https://metacpan.org/pod/Mojolicious::Plugin::Cron) uses standard Fcntl functions for that coordination, to assure
a platform-independent behavior.

# METHODS

[Mojolicious::Plugin::Cron](https://metacpan.org/pod/Mojolicious::Plugin::Cron) inherits all methods from
[Mojolicious::Plugin](https://metacpan.org/pod/Mojolicious::Plugin) and implements the following new ones.

## register

    $plugin->register(Mojolicious->new, {Cron => '* * * * *' => sub {}});

Register plugin in [Mojolicious](https://metacpan.org/pod/Mojolicious) application.

# WINDOWS INSTALLATION

To install in windows environments, you need to force-install module
Test::Mock::Time, or testings will fail.

# AUTHOR

Daniel Mantovani, `dmanto@cpan.org`

# COPYRIGHT AND LICENCE

Copyright 2018, Daniel Mantovani.

This library is free software; you may redistribute it and/or modify it under
the terms of the Artistic License version 2.0.

# SEE ALSO

[Mojolicious](https://metacpan.org/pod/Mojolicious), [Mojolicious::Guides](https://metacpan.org/pod/Mojolicious::Guides), [Mojolicious::Plugins](https://metacpan.org/pod/Mojolicious::Plugins), [Algorithm::Cron](https://metacpan.org/pod/Algorithm::Cron)
