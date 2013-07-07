---
layout: post
title: I hate JAXB.
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '766'
  original_post_id: '841'
  _wp_old_slug: '841'
---
My code:

<pre>
primaryPayment.setPaymentCode(paymentCode);
primaryPayment.setStart(convertDate(new Date()));
primaryPayment.setEnd(convertDate(endOfTime()));
primaryPayment.setSun(true);
primaryPayment.setMon(true);
primaryPayment.setTue(true);
primaryPayment.setWeds(true);
primaryPayment.setThur(true);
primaryPayment.setFri(true);
primaryPayment.setSat(true);
</pre>

My result:

<pre>
&lt;ns2:GuaranteePayment
  End="9999-12-31"
  Fri="true"
  Mon="true"
  PaymentCode="5"
  Sat="true"
  Start="2008-04-09"
  Sun="true"
  Thur="true"
  Tue="true"
  Type="GuaranteePolicy"
  Weds="true"
&gt;
</pre>

Wasn't XML supposed to be at least sort-of human readable?
