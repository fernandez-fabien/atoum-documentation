.. _variable-anchor:

variable
********

C'est l'assertion de base de toutes les variables. Elle contient les tests nécessaires à n'importe quel type de variable.

.. _variable-is-callable:

isCallable
==========

``isCallable`` vérifie que la variable peut être appelée comme fonction.

.. code-block:: php

   <?php
   $f = function() {
       // code
   };

   $this
       ->variable($f)
           ->isCallable()  // passe

       ->variable('\Vendor\Project\foobar')
           ->isCallable()

       ->variable(array('\Vendor\Project\Foo', 'bar'))
           ->isCallable()

       ->variable('\Vendor\Project\Foo::bar')
           ->isCallable()
   ;

.. _variable-is-equal-to:

isEqualTo
=========

``isEqualTo`` vérifie que la variable est égale à une certaine donnée.

.. code-block:: php

   <?php
   $a = 'a';

   $this
       ->variable($a)
           ->isEqualTo('a')    // passe
   ;


.. warning::
   | ``isEqualTo`` ne teste pas le type de la variable.
   | Si vous souhaitez vérifier également son type, utilisez :ref:`isIdenticalTo <variable-is-identical-to>`.


.. _variable-is-identical-to:

isIdenticalTo
=============

``isIdenticalTo`` vérifie que la variable a la même valeur et le même type qu'une certaine donnée. Dans le cas d'objets, ``isIdenticalTo`` vérifie que les données pointent sur la même instance.

.. code-block:: php

   <?php
   $a = '1';

   $this
       ->variable($a)
           ->isIdenticalTo(1)          // échoue
   ;

   $stdClass1 = new \StdClass();
   $stdClass2 = new \StdClass();
   $stdClass3 = $stdClass1;

   $this
       ->variable($stdClass1)
           ->isIdenticalTo(stdClass3)  // passe
           ->isIdenticalTo(stdClass2)  // échoue
   ;

.. warning::
   | ``isIdenticalTo`` teste le type de la variable.
   | Si vous ne souhaitez pas vérifier son type, utilisez :ref:`isEqualTo <variable-is-equal-to>`.


.. _variable-is-not-callable:

isNotCallable
=============

``isNotCallable`` vérifie que la variable ne peut pas être appelée comme fonction.

.. code-block:: php

   <?php
   $f = function() {
       // code
   };
   $int    = 1;
   $string = 'nonExistingMethod';

   $this
       ->variable($f)
           ->isNotCallable()   // échoue

       ->variable($int)
           ->isNotCallable()   // passe

       ->variable($string)
           ->isNotCallable()   // passe

       ->variable(new StdClass)
           ->isNotCallable()   // passe
   ;

.. _variable-is-not-equal-to:

isNotEqualTo
============

``isNotEqualTo`` vérifie que la variable n'a pas la même valeur qu'une certaine donnée.

.. code-block:: php

   <?php
   $a       = 'a';
   $aString = '1';

   $this
       ->variable($a)
           ->isNotEqualTo('b')     // passe
           ->isNotEqualTo('a')     // échoue

       ->variable($aString)
           ->isNotEqualTo($a)      // échoue
   ;

.. warning::
   | ``isNotEqualTo`` ne teste pas le type de la variable.
   | Si vous souhaitez vérifier également son type, utilisez :ref:`isNotIdenticalTo <variable-is-not-identical-to>`.


.. _variable-is-not-identical-to:

isNotIdenticalTo
================

``isNotIdenticalTo`` vérifie que la variable n'a ni le même type ni la même valeur qu'une certaine donnée.

Dans le cas d'objets, ``isNotIdenticalTo`` vérifie que les données ne pointent pas sur la même instance.

.. code-block:: php

   <?php
   $a = '1';

   $this
       ->variable($a)
           ->isNotIdenticalTo(1)           // passe
   ;

   $stdClass1 = new \StdClass();
   $stdClass2 = new \StdClass();
   $stdClass3 = $stdClass1;

   $this
       ->variable($stdClass1)
           ->isNotIdenticalTo(stdClass2)   // passe
           ->isNotIdenticalTo(stdClass3)   // échoue
   ;

.. warning::
   | ``isNotIdenticalTo`` teste le type de la variable.
   | Si vous ne souhaitez pas vérifier son type, utilisez :ref:`isNotEqualTo <variable-is-not-equal-to>`.


.. _is-null:

isNull
======

``isNull`` vérifie que la variable est nulle.

.. code-block:: php

   <?php
   $emptyString = '';
   $null        = null;

   $this
       ->variable($emptyString)
           ->isNull()              // échoue
                                   // (c'est vide, mais pas null)

       ->variable($null)
           ->isNull()              // passe
   ;

.. _is-not-null:

isNotNull
=========

``isNotNull`` vérifie que la variable n'est pas nulle.

.. code-block:: php

   <?php
   $emptyString = '';
   $null        = null;

   $this
       ->variable($emptyString)
           ->isNotNull()           // passe (c'est vide, mais pas null)

       ->variable($null)
           ->isNotNull()           // échoue
   ;

.. _is-not-true:

isNotTrue
=========

``isNotTrue`` vérifie que la variable n'est strictement pas égale à ``true``.

.. code-block:: php

   <?php
   $true  = true;
   $false = false;
   $this
       ->variable($true)
           ->isNotTrue()     // échoue

       ->variable($false)
           ->isNotTrue()     // passe
   ;


.. _is-not-false:

isNotFalse
==========

``isNotFalse`` vérifie que la variable n'est strictement pas égale à ``false``.

.. code-block:: php

   <?php
   $true  = true;
   $false = false;
   $this
       ->variable($false)
           ->isNotFalse()     // échoue

       ->variable($true)
           ->isNotFalse()     // passe
   ;
