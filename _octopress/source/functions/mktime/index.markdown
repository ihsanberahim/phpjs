---
layout: page
title: "JavaScript mktime function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/mktime:474
- /functions/view/mktime
- /functions/view/474
- /functions/mktime:474
- /functions/474
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's mktime

{% codeblock datetime/mktime.js lang:js https://raw.github.com/kvz/phpjs/master/functions/datetime/mktime.js raw on github %}
function mktime() {
  //  discuss at: http://phpjs.org/functions/mktime/
  // original by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // improved by: baris ozdil
  // improved by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // improved by: FGFEmperor
  // improved by: Brett Zamir (http://brett-zamir.me)
  //    input by: gabriel paderni
  //    input by: Yannoo
  //    input by: jakes
  //    input by: 3D-GRAF
  //    input by: Chris
  // bugfixed by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // bugfixed by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
  // bugfixed by: Marc Palau
  // bugfixed by: Brett Zamir (http://brett-zamir.me)
  //  revised by: Theriault
  //        note: The return values of the following examples are
  //        note: received only if your system's timezone is UTC.
  //   example 1: mktime(14, 10, 2, 2, 1, 2008);
  //   returns 1: 1201875002
  //   example 2: mktime(0, 0, 0, 0, 1, 2008);
  //   returns 2: 1196467200
  //   example 3: make = mktime();
  //   example 3: td = new Date();
  //   example 3: real = Math.floor(td.getTime() / 1000);
  //   example 3: diff = (real - make);
  //   example 3: diff < 5
  //   returns 3: true
  //   example 4: mktime(0, 0, 0, 13, 1, 1997)
  //   returns 4: 883612800
  //   example 5: mktime(0, 0, 0, 1, 1, 1998)
  //   returns 5: 883612800
  //   example 6: mktime(0, 0, 0, 1, 1, 98)
  //   returns 6: 883612800
  //   example 7: mktime(23, 59, 59, 13, 0, 2010)
  //   returns 7: 1293839999
  //   example 8: mktime(0, 0, -1, 1, 1, 1970)
  //   returns 8: -1

  var d = new Date(),
    r = arguments,
    i = 0,
    e = ['Hours', 'Minutes', 'Seconds', 'Month', 'Date', 'FullYear'];

  for (i = 0; i < e.length; i++) {
    if (typeof r[i] === 'undefined') {
      r[i] = d['get' + e[i]]();
      r[i] += (i === 3); // +1 to fix JS months.
    } else {
      r[i] = parseInt(r[i], 10);
      if (isNaN(r[i])) {
        return false;
      }
    }
  }

  // Map years 0-69 to 2000-2069 and years 70-100 to 1970-2000.
  r[5] += (r[5] >= 0 ? (r[5] <= 69 ? 2e3 : (r[5] <= 100 ? 1900 : 0)) : 0);

  // Set year, month (-1 to fix JS months), and date.
  // !This must come before the call to setHours!
  d.setFullYear(r[5], r[3] - 1, r[4]);

  // Set hours, minutes, and seconds.
  d.setHours(r[0], r[1], r[2]);

  // Divide milliseconds by 1000 to return seconds and drop decimal.
  // Add 1 second if negative or it'll be off from PHP by 1 second.
  return (d.getTime() / 1e3 >> 0) - (d.getTime() < 0);
}
{% endcodeblock %}

 - [Raw function on GitHub](https://github.com/kvz/phpjs/blob/master/functions/datetime/mktime.js)

Please note that php.js uses JavaScript objects as substitutes for PHP arrays, they are 
the closest match to this hashtable-like data structure. 

Please also note that php.js offers community built functions and goes by the 
[McDonald's Theory](https://medium.com/what-i-learned-building/9216e1c9da7d). We'll put online 
functions that are far from perfect, in the hopes to spark better contributions. 
Do you have one? Then please just: 

 - [Edit on GitHub](https://github.com/kvz/phpjs/edit/master/functions/datetime/mktime.js)


### Other PHP functions in the datetime extension
{% render_partial _includes/custom/datetime.html %}
