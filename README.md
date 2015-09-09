# js-mixin-inheritance
Javascript prototypal inheritance through mixin


(function(){
    'use strict';
    
	function Foo() {
    }
    
    Foo.prototype = {
    	y: 2,
        x: 3,
    	init: function() {
 			console.log('init');
 		},
 		callX: function() {
			alert(this.x);
		},
        callY: function() {
        	alert(this.y);
        }
    };
    
    function FooFoo() {
    }
    
    FooFoo.prototype = {
        z: 8,
    	callZ: function() {
        	alert(this.z);
        }
    };

	function Bar() {
    	Foo.call(this, 'init');  //super call
        FooFoo.call(this); //super call
    };

	Bar.prototype = Object.create(Foo.prototype);
	
    
	var baz = mixin(Bar.prototype, FooFoo.prototype);
	
    baz.init();
	baz.callY();
    
    function mixin() {
    	var src= arguments[0],
            objs = [].slice.call(arguments,1);
        
        for(var i =0 ,max = objs.length; i < max; i +=1) {
        	for(var key in objs[i]) {
            	if( !( key in src ) ) {
                    src[key] = objs[i][key];
                }
            }
        }
        
        return src;
    }
}());
