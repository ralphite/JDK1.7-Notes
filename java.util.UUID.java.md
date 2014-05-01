##java.util.UUID.java.md
----------------

represents the immutable universally unique identifier which is a 128bit value.

4 types of UUID

- time based
- DCE security
- name based
- randomly generated

> note assert is used in 107.

..

> note line 109 and 111. why do we need to & 0xff? it's for avoid overflow/downflow warnings

..

> note the many bit manip code
