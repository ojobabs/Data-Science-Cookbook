
```mermaid
graph TD;
P --> id6((Service Area))
subgraph two
C[agent_add_all.csv] -- org_unit == go --> D((geocode))
D --> H[agent_add_go_Geocoded.lyr]
H --> I((DeleteIdentical))
I --> J((DBSCAN))
J --> K[agent_add_go_HDBSCAN2.lyr]
K --> L((Remove outliers))
L --> M((% outliers))
M --> N{outliers == 20%?}
N -- Loop --> J
N --> O((Add marketer_id))
O --> P[marketers_go.lyr]
end
subgraph one
A[offices_all.csv] --> B((geocode)) 
B --> G[offices_all_Geocoded.lyr]
end
subgraph three
id1[clients_address_all.csv] -- general_office == go --> id2((geocode))
id2 --> id3[clients_address_add_go_Geocoded.lyr]
id3 --> id4((join marketer_id))
id4 --> id5[client_join_go.lyr]
id5 -- NO--> id6((Service Area))
id6 --> id7[SAPolygons1.lyr]
id7 --> id8((Rename))
id6 --> id9[LocalMarket_go.lyr]
id9 --> id10((Rename))
id10 --> id11[ServiceArea1.lyr]
id8 --> id12[LocalMarket_go.lyr]
id12 --> id13((Spatial Join))
id5 --> id13
id13 --> id14[Polygons_SpatialJoin_go.lyr]
id14 --> id15((% Clients inside LM))
id15 --> id16{% Clients == 50%?}
id16 -- Loop --> id6
id13 --> id17
id16 --> id17((Pop Density))
id17 --> id18[Plygons_pop_Den_go.lyr]
id18 --> id19((Metrics to CSV))
id19 --> id20[geo_loop_3.csv]
end
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTY4NjYyNTE4LC03NDc5MDM5MDgsMTYwNj
k0MTQwMyw4MzkyMzE3MTYsOTU1NTU0MDY4LC0xNDY0NDU5MzQs
LTUwMjE0ODQ5Nl19
-->