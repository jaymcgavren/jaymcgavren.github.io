---
layout: post
title: 'Ruby on Acid: YAML says it all...'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1062'
  original_post_id: '1336'
  _wp_old_slug: '1336'
---
<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/00021_random.png' title='00021_random.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/00021_random.png' alt='00021_random.png' /></a>

{% highlight yaml %}
--- !ruby/object:RubyOnAcid::MetaFactory
assigned_factories:
  :x2: &id001 !ruby/object:RubyOnAcid::LoopFactory
    counters:
      :x2: 0.0809003150016822
      :x: 0.0809003150016822
    interval: 0.0431080448196972
  :y: &id005 !ruby/object:RubyOnAcid::SineFactory
    counters:
      :y: -47.6973132292325
    interval: -0.0661543872804878
  :blue: &id004 !ruby/object:RubyOnAcid::SineFactory
    counters:
      :blue: -49.6672530194527
    interval: -0.0688866199992418
  :y2: &id006 !ruby/object:RubyOnAcid::SineFactory
    counters:
      :y2: -48.3512112649079
    interval: -0.067061319368805
  :alpha: &id002 !ruby/object:RubyOnAcid::LoopFactory
    counters:
      :alpha: 0.026577401239561
    interval: 0.0735458771168371
  :width: &id008 !ruby/object:RubyOnAcid::RepeatFactory
    repeat_count: 73.7486871161379
    repeat_counts:
      :width: 55
    source_factory: !ruby/object:RubyOnAcid::SineFactory
      counters:
        :width: -0.763070310680217
      interval: -0.0763070310680217
    values:
      :width: 0.154428166901605
  :red: &id003 !ruby/object:RubyOnAcid::FlashFactory
    counters:
      :red: 35
    interval: 48.2819400095083
    values:
      :red: 1.0
  :x: *id001
  :green: &id007 !ruby/object:RubyOnAcid::RepeatFactory
    repeat_count: 92.57504008154
    repeat_counts:
      :green: 70
    source_factory: !ruby/object:RubyOnAcid::LoopFactory
      counters:
        :green: 0.389712742634083
      interval: -0.0762859071707396
    values:
      :green: 0.389712742634083
factory_pool:
- !ruby/object:RubyOnAcid::LoopFactory
  counters: {}

  interval: 0.00689322163990813
- *id002
- !ruby/object:RubyOnAcid::LoopFactory
  counters: {}

  interval: -0.0330245624043419
- *id001
- !ruby/object:RubyOnAcid::ConstantFactory
  value: 0.799727962512452
- *id003
- *id004
- *id005
- !ruby/object:RubyOnAcid::SineFactory
  counters: {}

  interval: -0.04853454869413
- *id006
- *id007
- !ruby/object:RubyOnAcid::RepeatFactory
  repeat_count: 385.71501513496
  repeat_counts: {}

  source_factory: !ruby/object:RubyOnAcid::RandomFactory {}

  values: {}

- *id008
- !ruby/object:RubyOnAcid::ModuloFactory
  prior_values: {}

  source_factory: !ruby/object:RubyOnAcid::LoopFactory
    counters: {}

    interval: 1.0e-05
{% endhighlight %}
