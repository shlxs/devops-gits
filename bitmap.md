### wah ###
        +-----+------------------------------+
        | 1*  |******************************|  31 bit literal
        +-----+------------------------------+
        | 0*  |******************************|  number of 0 or 1 blocks (second bit indicate flag)
        +-----+------------------------------+

   block is word (32 or 64 bit).
   RLE of 0 or 1 block.
   
   
### concise ###

        +-----+-------+-------------------------+
        |type |   5              25             |
        +-----+-------+-------------------------+
        | 1*  | ******************************  |  31 bit literal
        +-----+-------+-------------------------+
        | 00  | ***** |*************************|  1 in first 32 bit | number of 0' blocks
        +-----+-------+-------------------------+
        | 01  | ***** |*************************|  0 in first 32 bit | number of 1' blocks
        +-----+-------+-------------------------+

   advantage: 
       space is always better than just save number array, and maybe
       save half space than wah.
      computation time is close to wah.
      
  
### ewah ###
     Running Length word | [literal words]*| Running Length word | [literal words]*
         
        +----------------+---------------+-------+
        |      16        |       15      |  1    |
        +----------------+---------------+-------+
        |****************|***************|  *    |
        +----------------+---------------+-------+
        |   blocks of    | literal words |running|
        |  running bits  |               | bits  |
        +----------------+---------------+-------+
  (For 64 bit system, 32 31 1)
  advantage:
    computation is simple and fast.
  usage: git/hive
### pwah ###
     8pwah 4-pwah 2pwah just like wah, but every word is divided into
     partitions. 2pwah is most used pwah.
     
     Better than wah for 64bit system.
     adaptive for different condition. (from bbc to wah)
summary
-------
different algorithm for concern
 
  - Concise for space
  - Ewah for computation
  - Wah for simplication
  - Pwah for 64bit and adaptive
