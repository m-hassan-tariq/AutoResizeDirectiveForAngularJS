# AutoResizeDirectiveForAngularJS
Custom directive that resize text area as per user key input or through paste/cut

Over the years I have seen many solutions for this problem, so I have written angualr directive to resolve this issue.
I have prefer vertical resize because horizontal resize strikes me as being a mess, due to word-wrap, long lines, and so on, 
but vertical resize seems to be pretty safe and nice. Please note instead of clientHeight attribute use scrollHeight

### Features
- On key input.
- With pasted text (right click & ctrl+v).
- With cut text (right click & ctrl+x).
- With pre-loaded text.
- With all textarea's (multiline textbox's) site wide.
- Is w3c validated.

Angular Code:

    (function () {
      'use strict';
   
      angular
          .module('sampleApp' , [])
          .directive('autoResize', autoResize);
   
          autoResize.$inject = ['$timeout'];
       
          function autoResize($timeout) {
       
              var directive = {
                  restrict: 'A',
                  link: function autoResizeLink(scope, element, attributes, controller) {
       
                      element.css({ 'height': 'auto', 'overflow-y': 'hidden' });
                      $timeout(function () {
                          element.css('height', element[0].scrollHeight + 'px');
                      }, 100);
       
                      element.on('input', function () {
                          element.css({ 'height': 'auto', 'overflow-y': 'hidden' });
                          element.css('height', element[0].scrollHeight + 'px');
       
                      });
                  }
              };
       
              return directive;
          };
    })();

Angular HTML Code:

    <textarea auto-resize style="resize: none;"></textarea>

#### Initial State:

![capture png](https://cloud.githubusercontent.com/assets/10474169/17199123/30ecc9e2-5440-11e6-8d3d-b0cea9e1b3e8.png)

#### After user input through keystrokes:

![capture](https://cloud.githubusercontent.com/assets/10474169/17199048/99190efa-543f-11e6-85b7-b217fc650755.PNG)

#### After user input through paste:

![capturez png](https://cloud.githubusercontent.com/assets/10474169/17199108/11f951c2-5440-11e6-9355-f02f172ee0e7.png)
