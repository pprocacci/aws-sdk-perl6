#!/usr/bin/env perl6

use IO::Glob;
use Template::Mustache;

sub MAIN(*@files)
{
  my %services;
  for @files || glob('botocore/botocore/data/*/*/service-2.json') {
    my $f;
    /$<f> = <-[/]>+ '/' $<g> = <-[/]>+ '/' service '-' 2 '.' json$/;
    if $<f>.chars <= 3 {
      $f = $<f>.uc;
      %services<<$f>> = 1;
    } else {
      $f = join('', $<f>.Str.split('-').map({.tc}));
      %services<<$f>> = 1;
    }
  }

  my $stache = Template::Mustache.new: :from<../views>;
  my @services = %services.keys.sort;
  say $stache.render('services', { services => @services });
}
