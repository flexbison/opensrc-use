# lttng install

## intall packget
   need install:
   lttng-rcu  read copy and update, it is a communication for threads
   lttng      lttng daemon 
   lttng-ust  user space use lib 
   lttv       view the trace data humanlity


## use in app

   1.editor template example
   
    "xxx.tp"
    
    TRACEPOINT_EVENT
    (
       mymodule1,
       tag1,
       TP_ARGS(
           const char*, msg
       ),
       TP_FIELDS(
           ctf_string(msg, msg)
       )
    )


    TRACEPOINT_EVENT
    (
       mymodule2,
       tag2,
       TP_ARGS(
           const char*, msg
       ),
       TP_FIELDS(
           ctf_string(msg, msg)
       )
    )

   2.genrate .h and .c by lttng gen tool. example

   ```
   lttng-gen-tp xxx.tp -o xxx.h -o xxx.c

   ```

   3.in your app add xxx.h xxx.c, include xxx.h in call point

   ```
        #include "xxx.h"
        
        void foo()
        {
            tracepoint(mymodule1, tag1, "foo_tag_begin");
            //blabla
            tracepoint(mymodule2, tag2, "foo_tag_begin");
        }
   ```
   
   4. add link library. -llttng-ust

## profile in back
   new bashe
   
   lttng create mynewseeion
   lttng enable-event -u -a  #set event we interst
   lttng start
   //start you programe, or operation app
   lttng stop

   lttng view
