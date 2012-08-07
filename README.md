Smart Time Ago
======================

Smart Time Ago is a little jQuery library to update the relative timestamps in your document intelligently. (e.g "3 hours ago").

It's originally built for https://pragmatic.ly/. 

It's inspired by another jQuery plugin http://timeago.yarp.com/ but give more flexibility and more intelligently.

Installation
------------

You can use it as a jQuery plugin. 

    Just copy the lib/timeago.js or src/timeago.coffee to your project folder then load it after jQuery.

Or if you use node, you can install it from npm.
  
    $ npm install -g smart-time-ago

Why Smart?
-------------

Smart Time Ago will check and update the relative time every 60000 millisecond (60 seconds) in the scope you specify at the beginning. Latter it will check the newest time in your scope then tune the checking time interval to a proper value. 

For example, if the newest time in the scope you specify is '2 hours ago'. There is no need to check and update the relative time every 60 seconds. Instead, Smart Time Ago will automaticly make the checking time interval longer to 30 minutes.

Rules:
  
  The newest time less than 44 minutes, the checking time interval will set to 1 minute.

  The newest time between 44 and 89 minutes, the checking time interval will set to 22 minutes.

  The newest time more between 90 minutes and 42 hours, the checking time interval will set to 30 minutes.

  The newest time more than 42 hours, the checking time interval will set to half day.

Usage
------------

By default Smart Time Ago will keep watching on the time elements with a class of timeago and a ISO8601 timestamp in datatime attribute:

    <time class="timeago" datetime="2012-07-18T07:51:50Z">about 8 hours ago</time>
    
You can initialize the smart-time-ago in global like:

    $().timeago();
    
It will watch all your relative time elements by only one TimeAgo instance.

Or you can use it in a specify scope like.
   
    <div class="timeLables">
     <time class="timeago" datetime="2012-07-18T07:51:50Z">about 8 hours ago</time>
     <time class="timeago" datetime="2012-07-18T06:51:50Z">about 9 hours ago</time>
    </div>
    
    $('.timeLables').timeago();
 
It will create one TimeAgo instance to update the time elements in the div with timeLables class.

However you can also create TimeAgo instance for every time element separately like:

    $('.timeago').timeago();

BTW if you need dynamic add the time element to your document without refreshing the page or you want to refresh the timeago manually. You might need call the refresh function to refresh the instance like:

    $().timeago('refresh');

    
Configuration
--------------

There are some default configuration in Smart Time Ago:

    $.fn.timeago.defaults = {
      selector: 'time.timeago',
      attr: 'datetime',
      dir: 'up',
      suffix: 'ago'
    };
    
The 'time.timeago' is the default selector to watch and update.

The 'datetime' is the default attribute to put the ISO8601 absolute time to parse.

The 'up' in dir means the elements in your scope is display by time desc. which means if the dir sets to 'up'. Smart Time Ago will treat the first element's time as the newest time to adjust the time interval. Oppositely if it set to 'down', Smart Time Ago will treat the last element's time as the newewst time.


The 'ago' in 'suffix' means the relative generated by Smart Time Ago will look like '3 hours ago'.
If you want the text looks like '3 hours from now', you might need change the 'suffix' to 'from now'.

You can change the default configurations by passing the options to
timeago function when initialize timeago like:

    $('.timeago').timeago({selector: 'span.timeago', attr: 'title', dir: 'down', suffix: 'from now'})


TODO
-----
Will create a gem to better support Rails project.

Thanks very much if you could contribute.


Credits
-------

![pragmatic.ly](https://pragmatic.ly/assets/vlogo.png)

Smart Time Ago is maintained and funded by [Pragmatic.ly](https://pragmatic.ly/ "Pragmatic.ly").

Thanks to all the contributors.

Copyright (c) 2012 Terry Tai, Pragmatic.ly (terry@pragmatic.ly, https://pragmatic.ly/)
