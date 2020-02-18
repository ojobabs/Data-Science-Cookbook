
```mermaid
graph TD;
P --> id4
subgraph two
C[agent_add_all.csv  ____] -- org_unit == go ___ --> D((geocode_))
D --> H[agent_add_go_Geocoded.lyr  ______]
H --> I((DeleteIdentical _))
I --> J((DBSCAN __ ))
J --> K[agent_add_go_HDBSCAN2.lyr _______]
K --> L((Remove outliers _))
L --> M((% outliers))
M --> N{outliers == 20%? ___}
N -- Loop _--> J
N --> O((Add marketer_id _))
O --> P[marketers_go.lyr _]
end
subgraph one
A[offices_all.csv _] --> B((geocode_)) 
B --> G[offices_all_Geocoded.lyr __]
end
subgraph three
id1[clients_address_all.csv  __] -- general_office == go  ____ --> id2((geocode_))
id2 --> id3[clients_address_add_go_Geocoded.lyr____]
id3 --> id4((join marketer_id ___))
id4 --> id5[client_join_go.lyr ____]
id5 --> id6((Service Area ___))
id6 --> id7[SAPolygons1.lyr ____]
id7 --> id8((Rename __))
id6 --> id9[LocalMarket_go.lyr ____]
id9 --> id10((Rename __))
id10 --> id11[ServiceArea1.lyr ____]
id8 --> id12[LocalMarket_go.lyr ____]
id12 --> id13((Spatial Join ___))
id5 --> id13
id13 --> id14[Polygons_SpatialJoin_go.lyr ______]
id14 --> id15((% Clients inside LM ____))
id15 --> id16{% Clients == 50% ____}
id16 -- Loop __ --> id6
id13 --> id17
id16 --> id17((Pop Density  __))
id17 --> id18[Plygons_pop_Den_go.lyr _____]
id18 --> id19((Metrics to CSV ___))
id19 --> id20[geo_loop_3.csv ___]
end
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyNTE3NDMwNiwtNTAyMTQ4NDk2XX0=
-->