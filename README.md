## What it is

A jQuery plugin in that helps better orient and navigate long pages by:

* Sticking the current header at the top of the screen (sticky headers)
* Displaying the header hierarchy (table of contents) by clicking the sticky header

## Why use it

The problem with long pages is that after scrolling a bit you forget which section or subsection you’re in. Then if you want to scroll back up to check on something you struggle to get back to where you were. Using this plugin solves these two problems.

## How to use it

You can clone the repository from github

  git clone https://github.com/PebbleRoad/sticky-headers-with-toc.git --recursive

### 1. Include jQuery and Javascript Files

  <script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
  <script src="stickyHeaders/jquery.stickyHeaders.js"></script>
  <script src="javascript-table-of-contents/toc.js"></script>

### 2. Your html structure


  <div class="container">

      <h2>Some main heading</h2>

      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Deleniti, nulla, eveniet, sint odit quas iusto sit veniam doloremque officia rem laudantium dolores cupiditate possimus accusamus odio. Architecto, sequi hic quidem.</p>

      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Deleniti, nulla, eveniet, sint odit quas iusto sit veniam doloremque officia rem laudantium dolores cupiditate possimus accusamus odio. Architecto, sequi hic quidem.</p>

      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Deleniti, nulla, eveniet, sint odit quas iusto sit veniam doloremque officia rem laudantium dolores cupiditate possimus accusamus odio. Architecto, sequi hic quidem.</p>

      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Deleniti, nulla, eveniet, sint odit quas iusto sit veniam doloremque officia rem laudantium dolores cupiditate possimus accusamus odio. Architecto, sequi hic quidem. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reprehenderit, mollitia, recusandae, distinctio molestiae maxime voluptatem ratione cumque maiores quas ullam veniam consequatur dolor repudiandae facere unde quaerat explicabo molestias praesentium!</p>

      <h2>Another main heading</h2>

      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Deleniti, nulla, eveniet, sint odit quas iusto sit veniam doloremque officia rem laudantium dolores cupiditate possimus accusamus odio. Architecto, sequi hic quidem. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reprehenderit, mollitia, recusandae, distinctio molestiae maxime voluptatem ratione cumque maiores quas ullam veniam consequatur dolor repudiandae facere unde quaerat explicabo molestias praesentium!</p>
  </div>



### 3. Initialize the plugin


    <script>
      $(function(){
          /**
           * Initialize Sticky header
           */

          $('.container').stickyHeaders({
              headlineSelector: 'h2, h3, h4, h5, h6'                    
          })

          /**
           * Add active class to table of contents on update
           */
          .bind('sticky-change', function(event, activeItem, isSticky){

              var activeToc = activeItem,
                  $toc = $('.list--toc').find('li').removeClass('active');

              if(isSticky){
                  $toc.filter('.toc-'+activeToc).addClass('active');
              }
              
          })
          /**
           * Add Click Handler to Sticky to toggle Table of Contents
           */
          .on('click', '.sticky-helper span, .sticky-helper .icon', function(e){
              $('.list--toc').toggle();
              e.preventDefault();
          })
          /**
           * Hide Table of Contents on Scroll Start                 
           */
          .bind('sticky-scroll-start', function(){

              $('.list--toc').hide();

          });


          /**
           * Initialize Table of Contents                 
           */
          new Toc({
              target: 'h2',
              content: '.container',
              depth: 6,
              appendTo: '.sticky-helper'
          });



      });
    </script>