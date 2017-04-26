<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgcb03ec5">1. Mtrx</a>
<ul>
<li><a href="#org45037ba">1.1. discription</a></li>
<li><a href="#org26dd077">1.2. create</a></li>
<li><a href="#orgd7ea34b">1.3. operation</a></li>
<li><a href="#org1fa1e6f">1.4. property</a></li>
<li><a href="#org66ca83c">1.5. static function</a></li>
<li><a href="#orga8940f8">1.6. function</a></li>
</ul>
</li>
</ul>
</div>
</div>


<a id="orgcb03ec5"></a>

# Mtrx


<a id="org45037ba"></a>

## discription

Mtrx is a calculation library for matrix.

The library has only an Object &#x2013; Mtrx.

Mtrx is extends Array, is arrays of Numbers.


<a id="org26dd077"></a>

## create

It is really easy to create a matrix object what you want.

    // No arguments, create a 1×1 random(0 ~ 1) matrix
    new Mtrx()
    // -> Mtrx [ [ 0.7173410249746024 ] ]
    
    // Get a number, create a n×n random(0 ~ 1) matrix
    new Mtrx(2)
    // -> Mtrx [
    //  [ 0.9028933497295337, 0.18980748816858917 ],
    //  [ 0.10859200880292263, 0.560035422729191 ] ]
    
    // Get two numbers, create a n×m random(0 ~ 1) matrix
    new Mtrx(2, 3)
    // -> Mtrx [
    //  [ 0.6974184450003136, 0.6402339494410889, 0.4553998131618524 ],
    //  [ 0.38759912033793165, 0.8904429716538196, 0.7449091649551736 ] ]
    
    // Get three numbers, create a n×m x matrix
    new Mtrx(3, 4, 9)
    // -> Mtrx [ [ 9, 9, 9, 9 ], [ 9, 9, 9, 9 ], [ 9, 9, 9, 9 ] ]
    
    // Get numbers array, create a diag matrix
    new Mtrx([2, 4, 6])
    // -> Mtrx [ [ 2, 0, 0 ], [ 0, 4, 0 ], [ 0, 0, 6 ] ]
    
    // Get a 2-order numbers array, create a matrix like the array
    new Mtrx([[1, 2, 3], [4, 5, 6]])
    // -> Mtrx [ [ 1, 2, 3 ], [ 4, 5, 6 ] ]
    
    // Get two numbers and a function expression, create a matrix by the expression
    new Mtrx(2, 3, (i, j) => i + j)
    // -> Mtrx [ [ 0, 1, 2 ], [ 1, 2, 3 ] ]


<a id="orgd7ea34b"></a>

## operation

Mtrx object is a Array-like object. So, you can operat it just like to operat a 2-order Array.

    const m = new Mtrx(2, 3, 0)
    // -> Mtrx [ [ 0, 0, 0 ], [ 0, 0, 0 ] ]
    
    m[1][1]
    // or
    m.of(1, 1)
    // -> 0
    
    m[0][1] = 1
    // -> Mtrx [ [ 0, 1, 0 ], [ 0, 0, 0 ] ]
    
    m.changeRows(2)
    // -> Mtrx [ [ 0, 1, 0 ], [ 0, 0, 0 ], [ 0, 0, 0 ], [ 0, 0, 0 ] ]
    m.changeRows(1, 6)
    // -> Mtrx [ [ 0, 1, 0 ], [ 0, 0, 0 ], [ 0, 0, 0 ], [ 0, 0, 0 ], [ 6, 6, 6 ] ]
    m.changeRows(-2)
    // -> Mtrx [ [ 0, 1, 0 ], [ 0, 0, 0 ], [ 0, 0, 0 ] ]
    
    
    m.changeCols(1)
    // -> Mtrx [ [ 0, 1, 0, 0 ], [ 0, 0, 0, 0 ], [ 0, 0, 0, 0 ] ]
    
    m.resetLike([[1, 2, 3], [4, 5, 6]])
    // -> Mtrx [ [ 1, 2, 3 ], [ 4, 5, 6 ] ]


<a id="org1fa1e6f"></a>

## property

Mtrx have many base properties.

    const m = new Mtrx(2, 3, (i, j) => (i === j) ? 1 : 0)
    // -> Mtrx [ [ 1, 0, 0 ], [ 0, 1, 0 ] ]
    const n = new Mtrx([
      [1, 2, 0],
      [3, 4, 4],
      [5, 6, 3]
    ])
    // -> Mtrx [ [ 1, 2, 0 ], [ 3, 4, 4 ], [ 5, 6, 3 ] ]
    
    m.rows  // -> 2
    m.cols  // -> 3
    
    n.T
    // Calculate transpose matrix, return a new Mtrx object
    // -> Mtrx [
    // [ 1, 3, 5 ],
    // [ 2, 4, 6 ],
    // [ 0, 4, 3 ]
    // ]
    
    m.rank  // -> 2
    
    m[0][0] = 0
    // -> Mtrx [ [ 0, 0, 0 ], [ 0, 1, 0 ] ]
    m.rank  // -> 1
    
    n.det  // -> 10
    m.det  // -> NaN
    // If the Mtrx object's rows and cols was not equal, det would be NaN
    
    n.LUP
    // -> { L: Mtrx [ [ 1, 0, 0 ], [ 0.2, 1, 0 ], [ 0.6, 0.5, 1 ] ],
    //      U: Mtrx [ [ 5, 6, 3 ], [ 0, 0.8, -0.6 ], [ 0, 0, 2.5 ] ],
    //      P: Mtrx [ [ 0, 0, 1 ], [ 1, 0, 0 ], [ 0, 1, 0 ] ] }
    n.LUP.L
    // -> Mtrx [ [ 1, 0, 0 ], [ 0.2, 1, 0 ], [ 0.6, 0.5, 1 ] ]
    
    n.inv
    // -> Mtrx [ [ -1.2, -0.6, 0.8 ], [ 1.1, 0.3, -0.4 ], [ -0.2, 0.4, -0.2 ] ]
    
    // If there is no corresponding matrix, you would get a Error.
    m.LUP
    m.inv
    m.compan
    // -> Error: ...


<a id="org66ca83c"></a>

## static function

all the static functions is Immutable.

    Mtrx.rand(2, 3)
    // like new Mtrx(n, m)
    // -> Mtrx [
    //  [ 0.6974184450003136, 0.6402339494410889, 0.4553998131618524 ],
    //  [ 0.38759912033793165, 0.8904429716538196, 0.7449091649551736 ] ]
    
    Mtrx.like([[1, 2, 3], [4, 5, 6]])
    // like new Mtrx(matrix)
    // -> Mtrx [ [ 1, 2, 3 ], [ 4, 5, 6 ] ]
    
    Mtrx.zeros(3, 3)
    // like new Mtrx(n, m, 0)
    // -> Mtrx [ [ 0, 0, 0 ], [ 0, 0, 0 ], [ 0, 0, 0 ] ]
    
    Mtrx.ones(3, 4)
    // like new Mtrx(n, m, 1)
    // -> Mtrx [ [ 1, 1, 1, 1 ], [ 1, 1, 1, 1 ], [ 1, 1, 1, 1 ] ]
    
    Mtrx.eye(3)
    // -> Mtrx [ [ 1, 0, 0 ], [ 0, 1, 0 ], [ 0, 0, 1] ]
    
    Mtrx.diag([2, 4, 6])
    // like new Mtrx(array)
    // -> Mtrx [ [ 2, 0, 0 ], [ 0, 4, 0 ], [ 0, 0, 6 ] ]
    
    const m = new Mtrx(2, 3, (i, j) => i + j)
    // -> Mtrx [ [ 0, 1, 2 ], [ 1, 2, 3 ] ]
    const n = Mtrx.clone(m)
    // -> Mtrx [ [ 0, 1, 2 ], [ 1, 2, 3 ] ]
    
    const a = new Mtrx([
      [1, 2, 3],
      [4, 5, 6],
      [7, 8, 9]
    ])
    Mtrx.cof(a, 0, 0)
    // -> Mtrx [ [ 5, 6 ], [ 8, 9] ]

    const n = [[0, 1, 2], [1, 2, 3]]
    const m = new Mtrx(n)
    // -> Mtrx [ [ 0, 1, 2 ], [ 1, 2, 3 ] ]
    
    
    Mtrx.isMtrx(n)     // -> false
    Mtrx.isMtrx(m)     // -> true
    
    Mtrx.isMtrxLike(n)     // -> true
    Mtrx.isMtrxLike(m)     // -> true
    Mtrx.isMtrxLike([[1, 2], [1]]);     // -> false
    Mtrx.isMtrxLike([['1', 2], [1, 2]]);     // -> false
    
    Mtrx.isDiag(m)     // -> false
    Mtrx.isDiag([[1, 0], [0, 4]]);     // -> true
    
    Mtrx.isSameShape(m, n)     // -> true
    Mtrx.isSameShape(m, new Mtrx([[1, 2], [3, 4]]))     // -> false

Base calculation:

    const m = new Mtrx([[1, 0, 0], [0, 1, 0], [0, 0, 1]])
    const n = new Mtrx([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
    
    // A + B
    Mtrx.add(m, n)
    // -> Mtrx [ [ 2, 2, 3 ], [ 4, 6, 6 ], [ 7, 8, 10 ] ]
    
    // A - B
    Mtrx.sub(m, n)
    // -> Mtrx [ [ 0, -2, -3 ], [ -4, -4, -6 ], [ -7, -8, -8 ] ]
    
    // A * n
    Mtrx.mul(m, 3)
    // -> Mtrx [ [ 3, 0, 0 ], [ 0, 3, 0 ], [ 0, 0, 3 ] ]
    
    // A · B
    Mtrx.mul(m, n)
    // -> Mtrx [ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ]
    
    // A / n   Or  A / B
    Mtrx.div(n, m)
    // -> Mtrx [ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ]


<a id="orga8940f8"></a>

## function

Following functions will always return a new Mtrx object.

    const m = new Mtrx([[1, 0, 0], [0, 1, 0], [0, 0, 1]])
    const n = new Mtrx([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
    
    m.add(n)
    // like Mtrx.add(m, n)
    
    m.sub(n)
    // like Mtrx.sub(m, n)
    
    m.mul(n)
    // or
    m.leftMul(n)
    // like Mtrx.mul(m, n)
    
    m.rightMul(n)
    // like Mtrx.mul(n, m)
    
    m.div(n)
    // like Mtrx.div(m, n)
    
    // cofactor
    n.cof(1, 1)
    // -> Mtrx [ [ 1, 3 ], [ 7, 9 ] ]

