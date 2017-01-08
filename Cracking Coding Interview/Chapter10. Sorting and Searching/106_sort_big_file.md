## 10.6 Sort Big File
Imagine that you have a 20GB file with one string per line. Explain how you would sort the file.

**Solution from the book:**

When an interviewer gives you a size of 20 gigabytes, it should tell you something. In this case, it suggests that they don't want you to bring all the data into memory.

So what do we do? We only bring part of the data into memory.

We'll divide the file into chunks, which are x megabytes each, where x is the amount of memory we have available. Each chunk is sorted separately and then saved back to the file system.

Once all the chunks are sorted, we merge the chunks, one by one. At the end, we have a fully sorted file.

This algorithm is known as **[external sort](http://www.geeksforgeeks.org/external-sorting/)**.

    Inputs:  
    input_file  : Name of input file. input.txt
    output_file : Name of output file, output.txt
    run_size : Size of a run (can fit in RAM)
    num_ways : Number of runs to be merged

    Output:
    1) Read input_file such that at most 'run_size' elements
       are read at a time. Do following for the every run read
       in an array.
          a) Sort the run using MergeSort.
          b) Store the sorted run in a temporary file, say 'i' 
             for i'th run.
    2) Merge the sorted files using the approach discussed here
