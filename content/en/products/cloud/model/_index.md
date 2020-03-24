---
title: "Asset Model"
linkTitle: "Asset Model"
type: docs
weight: 2
draft: true
description: >
  How to integrate, structure and perform advanced analytics on your data.
---

WideSky Cloud is used to collect and analyse time-series data from a wide variety of devices and equipment. In order to organise this data, WideSky builds a [directed graph structure](https://en.wikipedia.org/wiki/Directed_graph) of all the devices (Assets) for which data is collected from. This Asset Model maintains the relationships between the devices and other important information about the devices like descriptions, unit of measures, or anything that is of worth.

Asset Model
At it's core, the asset model is a database that stores information about the "Things" that require representation, and the relationship between them. These things could be pieces of equipment, sensors within a piece of equipment, a location grouping things together, basically any physical object can be represented and within the Asset Model, an object is referred as the term entity.

Entities can be anything. Objects like sites, pieces of equipment, sensor points and weather stations can all be represented by an entity.


{{% alert title="Note"  color="primary" %}} A key characteristic of the asset model is that it is designed to be machine-readable as easily as it is human-readable, and that has some powerful consequences in terms of the sorts of automated analysis that can be performed later.
{{% /alert %}}

To distinguish between these entities, the Asset Model takes a tag based approach. This means that rather than enforcing a (top-down) hierarchy, a (bottom-up) tag-based approach allows for much more flexibility and richness in the way entities are organised. Tags are simply name value pairs that get associated with entities, enabling identification, categorisation and grouping.

The Asset Model uses a special 'Marker' tag to categorise entities, and entities can have multiple marker tags. For example, an entity might use the "equip" marker tag to represent that it is a piece of equipment, the "meter" tag to classify it as metering equipment, and the "elec" tag to indicate it is an electrical meter. If the meter is a site level (main incomer) meter, we can attach the "siteMeter" marker tag. If the entity is a sensor collecting data, we can attach the "point" marker tag. To this we can also add the "dis" tag to attach a descriptive name for the device.

Entities can be linked by using the special ref tag with it's value being an identifier of the entity being referenced.
