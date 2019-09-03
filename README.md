# Python_code
# This is the python code for the question for medium level python coders
""" Question:Given a set of points on a map, find out the most optimal way to travel between the points. Ignore the need to travel by road. Assume that you can fly. 
 Now, if we constrain order by time too how would you change the code.
 The Code should not be more than 250 lines and it should be built in Django Framework and should be deployed on a web server."""

# this problem is assumed to be of a type of Travelling salesperson problem
import doctest
from itertools import permutations

# In this code we have assumed a map to be a x-y cartesian plane in which a point(assumed to be of a location in a map) has its coordinates.

def distance(point1, point2):
    """
    Returns the Euclidean distance of two points in the Cartesian Plane.

    -> distance([3,4],[0,0])
    5.0
    -> distance([3,6],[10,6])
    7.0
    """
    return ((point1[0] - point2[0])**2 + (point1[1] - point2[1])**2) ** 0.5

def total_distance(points):
    """
    Returns the length of the path passing throught
    all the points in the given order.

    -> total_distance([[1,2],[4,6]])
    5.0
    -> total_distance([[3,6],[7,6],[12,6]])
    9.0
    """
    return sum([distance(point, points[index + 1]) for index, point in enumerate(points[:-1])])
    
    # function for finding out the most optimal way to travel between a given set of points
def travelling_salesman(points, start=None):
    """
    Finds the shortest route to visit all the cities by bruteforce.

    -> travelling_salesman([[0,0],[10,0],[6,0]])
    ([0, 0], [6, 0], [10, 0])
    -> travelling_salesman([[0,0],[6,0],[2,3],[3,7],[0.5,9],[3,5],[9,1]])
    ([0, 0], [6, 0], [9, 1], [2, 3], [3, 5], [3, 7], [0.5, 9])
    """
    if start is None:
        start = points[0]
    return min([perm for perm in permutations(points) if perm[0] == start], key=total_distance)

def main():
    doctest.testmod()
    points = [[0, 0], [9, 5.45], [6, 3], [16, 7.2],            # coordinates could be changed according to the given location 
              [0.5, 4.56], [5, 5], [8, 1], [10, 13]]           # different inputs could be given consisting of different no. of locations
    print("""The minimum distance to visit all the following points: {}
starting at {} is {}.""".format(
        tuple(points),
        points[0],
        total_distance(travelling_salesman(points))))

    
    
    
if __name__== "__main__":
    main()
