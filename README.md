Event
=====

实现了事件的绑定以及解绑，一次绑定事件

            Event=function(obj){
            	var event={};
            	obj=obj||{};
            	obj.on=function(type,fn,isonce){
            		var handler={
            			id:new Date()+0,
            			callback:fn;
            			isonce:isonce||false
            		}
            		if(event[type]){
            			event[type].push(handler);
            		}else{
            			event[type]=[handler];
            		}
            		return  handler.id;
            	};
            	obj.once=function(type,fn){
            		obj.on(type,fn,true);
            	};
            	obj.off=function(type,handle){
            		if(event[type]){
            			var l=event[type].length;
            			for(var i=0;i<l;i++ ){
            				if(event[type][i].id==handle)event[type].splice(i,1);
            			}
            		}a
            	};
            	obj.emit=function(type,data){
            		if(event[type]){ 
            			for(var i=0;i<event[type].length;i++){
            				var handler=event[type][i];
            				handler.callback.call(obj,data);
            				if(handler.isonce){
            				   obj.off(type,handler)
            				}
            			}
            		}
            	};
            }
