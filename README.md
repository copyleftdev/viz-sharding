# Visual Guide to Sharding Algorithms

This guide provides advanced visual representations of key sharding algorithms using Mermaid charts. Sharding, a critical strategy for scaling databases, involves splitting large datasets into smaller, more manageable pieces (shards). This visualization highlights various sharding algorithms, showcasing their approaches for distributing data across shards. Each chart provides a structural flow of the algorithm, making it easier to grasp sharding strategies.

## 1. Hash-Based Sharding

Hash-based sharding is one of the most common strategies, where a hash function is used to determine the shard location.

```mermaid
graph TD
    subgraph HashFunction
        A[Start] --> B["Compute hash(key)"]
        B --> C["Calculate shard number:<br/>hash(key) % total_shards"]
        C --> D{"Shard Number"}
        D --> E["Store data in shard"]
    end
    
    subgraph Shards
        F["Shard 1"]
        G["Shard 2"]
        H["Shard 3"]
        I["Shard 4"]
    end
    
    C -.->|0| F
    C -.->|1| G
    C -.->|2| H
    C -.->|3| I
    
    style F fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:2px
    style H fill:#fbf,stroke:#333,stroke-width:2px
    style I fill:#bfb,stroke:#333,stroke-width:2px
```

## 2. Range-Based Sharding

Range-based sharding uses ordered ranges of values to decide shard allocation.

```mermaid
graph TD
    subgraph RangeFunction
        A[Start] --> B["Check value range"]
        B --> C{"Value in range 1?"}
        C -->|Yes| D["Assign to Shard 1"]
        C -->|No| E{"Value in range 2?"}
        E -->|Yes| F["Assign to Shard 2"]
        E -->|No| G{"Value in range 3?"}
        G -->|Yes| H["Assign to Shard 3"]
        G -->|No| I["Assign to Shard 4"]
    end
    
    subgraph Shards
        J["Shard 1: 0-1000"]
        K["Shard 2: 1001-2000"]
        L["Shard 3: 2001-3000"]
        M["Shard 4: 3001+"]
    end
    
    D -.-> J
    F -.-> K
    H -.-> L
    I -.-> M

    style J fill:#f9f,stroke:#333,stroke-width:2px
    style K fill:#bbf,stroke:#333,stroke-width:2px
    style L fill:#fbf,stroke:#333,stroke-width:2px
    style M fill:#bfb,stroke:#333,stroke-width:2px
```

## 3. Directory-Based Sharding

In directory-based sharding, a central directory maps keys to shards.

```mermaid
graph TD
    subgraph Directory
        A[Start] --> B["Lookup directory for key"]
        B --> C{"Key found?"}
        C -->|Yes| D["Retrieve shard number"]
        C -->|No| E["Add key to directory"]
        E --> F["Map key to new shard"]
        F --> D
        D --> G["Store data in shard"]
    end

    subgraph Shards
        H["Shard 1"]
        I["Shard 2"]
        J["Shard 3"]
        K["Shard 4"]
    end
    
    D -.->|1| H
    D -.->|2| I
    D -.->|3| J
    D -.->|4| K

    style H fill:#f9f,stroke:#333,stroke-width:2px
    style I fill:#bbf,stroke:#333,stroke-width:2px
    style J fill:#fbf,stroke:#333,stroke-width:2px
    style K fill:#bfb,stroke:#333,stroke-width:2px
```

## 4. Entity-Based Sharding

Entity-based sharding places related data in the same shard based on an entity relationship, such as user ID or account.

```mermaid
graph TD
    subgraph EntityRelation
        A[Start] --> B["Identify related entity"]
        B --> C{"Entity already sharded?"}
        C -->|Yes| D["Use existing shard"]
        C -->|No| E["Create new shard for entity"]
        E --> D
        D --> F["Store data in shard"]
    end

    subgraph Shards
        G["User 1 Data"]
        H["User 2 Data"]
        I["User 3 Data"]
        J["New User Shard"]
    end
    
    D -.->|1| G
    D -.->|2| H
    D -.->|3| I
    D -.->|4| J

    style G fill:#f9f,stroke:#333,stroke-width:2px
    style H fill:#bbf,stroke:#333,stroke-width:2px
    style I fill:#fbf,stroke:#333,stroke-width:2px
    style J fill:#bfb,stroke:#333,stroke-width:2px
```

## 5. Geographical Sharding

Geographical sharding distributes data based on location.

```mermaid
graph TD
    subgraph GeoFunction
        A[Start] --> B["Check geographical location"]
        B --> C{"Region: North America?"}
        C -->|Yes| D["Assign to Shard 1"]
        C -->|No| E{"Region: Europe?"}
        E -->|Yes| F["Assign to Shard 2"]
        E -->|No| G{"Region: Asia?"}
        G -->|Yes| H["Assign to Shard 3"]
        G -->|No| I["Assign to Shard 4"]
    end

    subgraph Shards
        J["Shard 1: North America"]
        K["Shard 2: Europe"]
        L["Shard 3: Asia"]
        M["Shard 4: Others"]
    end

    D -.-> J
    F -.-> K
    H -.-> L
    I -.-> M

    style J fill:#f9f,stroke:#333,stroke-width:2px
    style K fill:#bbf,stroke:#333,stroke-width:2px
    style L fill:#fbf,stroke:#333,stroke-width:2px
    style M fill:#bfb,stroke:#333,stroke-width:2px
```

## 6. Consistent Hashing

Consistent hashing reduces reallocation when adding or removing shards, ensuring minimal movement of keys.

```mermaid
graph TD
    subgraph ConsistentHash
        A[Start] --> B["Compute hash(key)"]
        B --> C["Locate closest node in ring"]
        C --> D["Assign key to closest node"]
    end

    subgraph Ring
        E["Node 1"]
        F["Node 2"]
        G["Node 3"]
        H["Node 4"]
    end
    
    C -.-> E
    C -.-> F
    C -.-> G
    C -.-> H

    style E fill:#f9f,stroke:#333,stroke-width:2px
    style F fill:#bbf,stroke:#333,stroke-width:2px
    style G fill:#fbf,stroke:#333,stroke-width:2px
    style H fill:#bfb,stroke:#333,stroke-width:2px
```

## 7. Time-Based Sharding

Time-based sharding stores data based on temporal ranges.

```mermaid
graph TD
    subgraph TimeFunction
        A[Start] --> B["Check timestamp"]
        B --> C{"Month: January?"}
        C -->|Yes| D["Assign to Shard 1"]
        C -->|No| E{"Month: February?"}
        E -->|Yes| F["Assign to Shard 2"]
        E -->|No| G{"Month: March?"}
        G -->|Yes| H["Assign to Shard 3"]
        G -->|No| I["Assign to Shard 4"]
    end

    subgraph Shards
        J["Shard 1: January"]
        K["Shard 2: February"]
        L["Shard 3: March"]
        M["Shard 4: Other Months"]
    end

    D -.-> J
    F -.-> K
    H -.-> L
    I -.-> M

    style J fill:#f9f,stroke:#333,stroke-width:2px
    style K fill:#bbf,stroke:#333,stroke-width:2px
    style L fill:#fbf,stroke:#333,stroke-width:2px
    style M fill:#bfb,stroke:#333,stroke-width:2px
```

This guide provides a comprehensive overview of sharding strategies, offering visual insights for advanced understanding of sharding techniques.
