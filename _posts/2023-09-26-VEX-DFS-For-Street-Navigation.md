// user inputs
float targetlen = @motionlength;
int startpt = nearpoint(1, @P);

// in this implementation, nodes are primitive endpoints
int visited[]; // nodes that have allready been visited
int stack[] = array(startpt); // the stack where candidate nodes are stored
dict nodemap = {}; // the dict that stores the nodes traversed
dict primmap = {};
dict lengthmap = {};
int nodesequence[];
int primsequence[];
float lentest;

float randcounter = 1; // a counter to add randomness based on iteration
while(len(stack) > 0)//for(int i = 0; i < chi("iter"); i++)
{
    randcounter++;
    int node = pop(stack);
    // if node node not visited
    if(find(visited, node) < 0)
    {
        append(visited, node);  
        
        // get length by looping through map until the start point is reached
        float length = 0;
        int nodepath[];
        int primpath[];
        int currpt = node;
        append(nodepath, node);
        while(currpt != startpt)
        {
            int child = nodemap[itoa(currpt)];
            length += lengthmap[itoa(currpt)];
            int primchild = primmap[itoa(currpt)];
            append(primpath, primchild);
            append(nodepath, child);
            currpt = child;

        }
          
        // break loop is desired length is reached
        if(length >= targetlen)
        {
            primsequence = primpath;
            nodesequence = nodepath;
            lentest = length;
            break;
        }
        
        int neighbourprims[] = pointprims(1, node);
        // add simple randomization
        float rand = rand(@ptnum * chf("seed")+.001 * randcounter) * chi("dfsrandom");
        if(rand > .5) neighbourprims = reverse(neighbourprims);
        
        int numneighbours = len(neighbourprims);
        foreach(int prim; neighbourprims)
        {
            int primstartpt = primpoints(1, prim)[0];
            int primendpt = primpoints(1, prim)[-1];
            int neighbournode; 
            if(primstartpt == node) neighbournode = primendpt;
            else neighbournode = primstartpt;
            if(find(visited, neighbournode) < 0)
            {
                append(stack, neighbournode);
                nodemap[itoa(neighbournode)] = node;
                primmap[itoa(neighbournode)] = prim;
                float primlength = prim(1, "length", prim);
                lengthmap[itoa(neighbournode)] = primlength;
            }
        }    
    }
}

i[]@primsequence = reverse(primsequence);
// f@lentest = lentest;
// i[]@nodesequence = nodesequence;
// d@nodemap = nodemap;
// d@primmap = primmap;
//d@lengthmap = lengthmap;
// i[]@visited = visited;
// i[]@stack = stack;