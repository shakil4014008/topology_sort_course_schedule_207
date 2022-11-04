# topology_sort_course_schedule_207


````CanFinish
def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:

        # initializing empty variables
        graph = {course: [] for course in range(numCourses)}
        indegree = {course:0 for course in range(numCourses)}
        zero_indegree_nodes = []

        # create a directed graph. [a,b]: b->a
        for a,b in prerequisites:
            graph[b].append(a)
            indegree[a] += 1

        # collect all nodes with zero indegree
        for course in indegree:
            if indegree[course] == 0:
                zero_indegree_nodes.append(course)
        
        # perform topological sort
        completed_courses = 0
        while zero_indegree_nodes:
            course = zero_indegree_nodes.pop(0) # this is a queue, as item popped from first element 
            completed_courses += 1
            for nei in graph[course]:
                indegree[nei] -= 1
                if indegree[nei] == 0:
                    zero_indegree_nodes.append(nei)
        
        # no nodes with zero indegree and some courses are still remaning to be completed => indicates cycle
        if len(zero_indegree_nodes) == 0 and completed_courses < numCourses:
            return False

        # otherwise no cycle
        return True
````
