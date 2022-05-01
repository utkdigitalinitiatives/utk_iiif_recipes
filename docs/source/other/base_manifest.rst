Base Manifest
=============

About
-----

This document describes rules that tend to be inherited by all content models unless otherwise specified in the model's
corresponding doc or in the specific property definition below.

Root Properties
---------------

`IIIF Assemble <https://github.com/utkdigitalinitiatives/iiif_assemble>`_ generates these properties at the root level
of the manifest.  Practices follow the `IIIF Presentation v3 Specification <https://iiif.io/api/presentation/3.0/>`_ and
the `Cookbook of IIIF Recipes <https://iiif.io/api/cookbook/>`_.

========
@context
========

The context property is always the first property in the manifest. For UTK collections, it is always an array with
:code:`https://iiif.io/api/presentation/3/context.json` as the last value (unless it is the only value).  Any other
extensions we use appear before this value. As of May 1, 2022, no other extensions are used.

See `4.6 Linked Data Context and Extensions <https://iiif.io/api/presentation/3.0/#46-linked-data-context-and-extensions>`_.

==
id
==

The :code:`id` property is a technical property that identifies the resource.  At the manifest level, this is always the
:code:`https` uri to the Manifest. (e.g. :code:`https://digital.lib.utk.edu/assemble/manifest/acwiley/280`)

IIIF Assemble translates this value and creates a dereferenceable IIIF manifest at this URI based on two patterns. For
collection objects, the pattern is :code:`https://digital.lib.utk.edu/assemble/collection/` plus the persistent identifier
(PID) of the object with the :code:`:` replaced with a :code:`/`.
(e.g. :code:`https://digital.lib.utk.edu/assemble/collection/collections/rfta`)

See `3.2. Technical Properties: id <https://iiif.io/api/presentation/3.0/#id>`_ for more information.

====
type
====

The :code:`type` property describes the type of class of the resource. The value is always a string. If the object is
not a collection, this value is always :code:`Manifest` at root.  Otherwise, it is :code:`Collection`.

See `3.2. Technical Properties: type <https://iiif.io/api/presentation/3.0/#type>`_ for more information.

=====
label
=====

The :code:`label` property is descriptive and is required at root on the manifest. Follow the presentation v3 specification,
the value MUST be a JSON object.

For UTK collections, this value is always the following where :code:`TITLE OF OBJECT` is equal to the value(s) of the
xpath expression :code:`titleInfo[not(@type="alternative")][not(@lang)]` expressed against the MODS record of the
related digital object:

.. code-block:: json

    {
        "en":
            ["TITLE OF OBJECT"]
    }

See `3.1. Descriptive Properties: label <https://iiif.io/api/presentation/3.0/#label>`_ for more information.

=======
summary
=======

The :code:`summary` property is a short textual summary intended to be conveyed to the user when the :code:`metadata`
entries for the resource are not being displayed. This could be used as a brief description for item level search
results, for small-screen environments, or as an alternative user interface when the :code:`metadata` property is not
currently being rendered.

The :code:`summary` property follows the same patten as label. If the expression :code:`abstract[not(@lang)]` against a
digital object's MODS record has a value, a summary is added to the manifest like this:

.. code-block:: json

    {
        "en":
            ["SUMMARY"]
    }

See `3.1. Descriptive Properties: summary <https://iiif.io/api/presentation/3.0/#summary>`_ for more information.

======
rights
======

The :code:`rights` property is a string that identifies a license or rights statement that applies to the content of the
digital object. It is modelled as a string.

The value of :code:`rights` is present if the XPATH expression :code:`accessCondition[@xlink:href]` against the object's
MODS record has a value.

See `3.1. Descriptive Properties: rights <https://iiif.io/api/presentation/3.0/#rights>`_ for more information.