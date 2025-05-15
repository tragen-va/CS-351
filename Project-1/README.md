
Program   | Optimization | Real (s) | User (s) | Sys (s) | Mem (KB) | Throughput (MH/s) | Speedup
----------|--------------|----------|----------|---------|----------|--------------------|---------
hash-00   | -g           | 122.73   | 119.60   | 3.11    | 3474     | 8.15               | 1.00
hash-01   | -g           | 6.83     | 5.92     | 0.90    | 3484     | 146.42             | 17.97
hash-02   | -g           | 7.40     | 6.52     | 0.86    | 3612     | 135.14             | 16.11
hash-03   | -g           | 5.91     | 5.06     | 0.84    | 3484     | 169.20             | 20.80
hash-04   | -g           | 6.31     | 5.95     | 0.35    | 5012572  | 158.47             | 19.34
hash-00   | -O2          | 121.51   | 118.30   | 3.19    | 3348     | 8.23               | 1.00
hash-01   | -O2          | 4.77     | 3.88     | 0.87    | 3776     | 209.64             | 25.47
hash-02   | -O2          | 4.74     | 3.84     | 0.89    | 3612     | 210.97             | 25.63
hash-03   | -O2          | 4.73     | 3.82     | 0.89    | 3476     | 211.39             | 25.68
hash-04   | -O2          | 5.61     | 3.90     | 1.69    | 5012476  | 178.25             | 21.64




1) It is probably so slow because of these lines 

            input >> byte;
            hash += (multiplier * byte) ^ (hash >> 23);

they read in the values manually 1 at a time and convert. This is very repetative and ineficient.


2) There is not much difference between the 2. hash-01 uses new while hash-02 uses alloc. Alloc is generlaly going to be slightly faster, whihc is shown by that fact hash-02 finished first. However they both took about 4.7 second so at this input size the gap is just within margin of error. 

3) Depends on your definition of appreciable. Hash-03 does consistantly finish before before hash-01 or hash-02, but by a very small margin, especailly with optimazation applied. The difference is neglagable. 

4) Hash-04 uses map() to map the entier input file into the processes area of memory, thus taking up alot more memory than reading it peice by piece. 


5)
