# python search & sort algorithms

> This is a simple list of python algorithms based on those I've used in other languages and seen in reference materials

### merge sort
	def mergeSort(alist):
	    print("Splitting ",alist)
	    if len(alist)>1:
	        mid = len(alist)//2
	        lefthalf = alist[:mid]
	        righthalf = alist[mid:]
	
	        mergeSort(lefthalf)
	        mergeSort(righthalf)
	
	        i=0
	        j=0
	        k=0
	        while i < len(lefthalf) and j < len(righthalf):
	            if lefthalf[i] < righthalf[j]:
	                alist[k]=lefthalf[i]
	                i=i+1
	            else:
	                alist[k]=righthalf[j]
	                j=j+1
	            k=k+1
	
	        while i < len(lefthalf):
	            alist[k]=lefthalf[i]
	            i=i+1
	            k=k+1
	
	        while j < len(righthalf):
	            alist[k]=righthalf[j]
	            j=j+1
	            k=k+1
	    print("Merging ",alist)
	
	alist = [54,26,93,17,77,31,44,55,20]
	mergeSort(alist)

### heap sort
 
	 def heapsort( aList ):
	  # convert aList to heap
	  length = len( aList ) - 1
	  leastParent = length / 2
	  for i in range ( leastParent, -1, -1 ):
	    moveDown( aList, i, length )
	 
	  # flatten heap into sorted array
	  for i in range ( length, 0, -1 ):
	    if aList[0] > aList[i]:
	      swap( aList, 0, i )
	      moveDown( aList, 0, i - 1 )
	 
	def moveDown( aList, first, last ):
	  largest = 2 * first + 1
	  while largest <= last:
	    # right child exists and is larger than left child
	    if ( largest < last ) and ( aList[largest] < aList[largest + 1] ):
	      largest += 1
	 
	    # right child is larger than parent
	    if aList[largest] > aList[first]:
	      swap( aList, largest, first )
	      # move down to largest child
	      first = largest;
	      largest = 2 * first + 1
	    else:
	      return # force exit

	def swap( A, x, y ):
	  tmp = A[x]
	  A[x] = A[y]
	  A[y] = tmp

### bubble sort
	
	def bubbleSort(alist):
	    for passnum in range(len(alist)-1,0,-1):
	        for i in range(passnum):
	            if alist[i]>alist[i+1]:
	                temp = alist[i]
	                alist[i] = alist[i+1]
	                alist[i+1] = temp
	
	alist = [54,26,93,17,77,31,44,55,20]
	bubbleSort(alist)
	print(alist)



 
### binary search
 
 
	def binarySearch(alist, item):
	    if len(alist) == 0:
	        return False
	    else:
	        midpoint = len(alist)//2
	        if alist[midpoint]==item:
	          return True
	        else:
	          if item<alist[midpoint]:
		            return binarySearch(alist[:midpoint],item)
		          else:
		            return binarySearch(alist[midpoint+1:],item)
		
	testlist = [0, 1, 2, 8, 13, 17, 19, 32, 42, 56]
	print(binarySearch(testlist, 3))
	print(binarySearch(testlist, 19))
 
### linear search
 
	def linearSearch(obj, item, start=0):
	    for i in range(start, len(obj)):
	        if obj[i] == item:
	            return i
	    return -1

### ordered sequential search
	
	def orderedSequentialSearch(alist, item):
	    pos = 0
	    found = False
	    stop = False
	    while pos < len(alist) and not found and not stop:
	        if alist[pos] == item:
	            found = True
	        else:
	            if alist[pos] > item:
		                stop = True
		            else:
		                pos = pos+1
		
		    return found
		
		testlist = [0, 1, 2, 8, 13, 17, 19, 32, 42,56]
		print(orderedSequentialSearch(testlist, 3))
		print(orderedSequentialSearch(testlist, 13))


# graph search
> a collection of graph search algorithms in python

	graph = {'a': set(['b', 'c']),
	         'b': set(['a', 'd', 'e']),
	         'c': set(['a', 'f']),
	         'd': set(['b']),
	         'e': set(['b', 'f']),
	         'f': set(['c', 'e'])}

	def depthFirstSearch(graph, start, visited=None):
	    if visited is None:
	        visited = set()
	    visited.add(start)
	    for next in graph[start] - visited:
	        depthFirstSearch(graph, next, visited)
	    return visited
	
	depthFirstSearch(graph, 'c')            # {'e', 'd', 'f', 'a', 'c', 'b'}
	
	def depthPaths(graph, start, goal):
	    stack = [(start, [start])]
	    while stack:
	        (vertex, path) = stack.pop()
	        for next in graph[vertex] - set(path):
	            if next == goal:
	                yield path + [next]
	            else:
	                stack.append((next, path + [next]))
	
	list(depthPaths(graph, 'a', 'f'))       # [['a', 'c', 'f'], ['a', 'b', 'e', 'f']]

### bread-first search
	
	def breadthFirstSearch(graph, start):
	    visited, queue = set(), [start]
	    while queue:
	        vertex = queue.pop(0)
	        if vertex not in visited:
	            visited.add(vertex)
	            queue.extend(graph[vertex] - visited)
	    return visited
	
	breadthFirstSearch(graph, 'a') # {'b', 'c', 'a', 'f', 'd', 'e'}
	
	def breadthFirstLines(graph, start, goal):
	    queue = [(start, [start])]
	    while queue:
	        (vertex, line) = queue.pop(0)
	        for next in graph[vertex] - set(line):
	            if next == goal:
	                yield line + [next]
	            else:
	                queue.append((next, line + [next]))
	
	list(breadthFirstLines(graph, 'a', 'f')) # [['a', 'c', 'f'], ['a', 'b', 'e', 'f']]
	
	def shortestLine(graph, start, goal):
	    try:
	        return next(bfs_paths(graph, start, goal))
	    except StopIteration:
	        return None
	
	shortestLine(graph, 'a', 'f') # ['a', 'c', 'f']
