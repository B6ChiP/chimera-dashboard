# chimera-dashboard
## Project Website
You can view the live website here:  
[Chimera Performance Metrics Website](https://www.cs.umb.edu/~hdeblois/cs410/longproj02/t6/#documentation)

## Dev Guide
1. Install npm
2. Install npm dependencies
```bash
npm install
```
3. You can automatically have tailwindcss watch your changes with the following command:
```bash
npm run watch-css
```
4. The `index.html` and `styles.css` can be found in `src/` directory.

```mermaid
flowchart LR
    %% Define Nodes and Subgraphs
    subgraph chimera ["chimera.umb.edu"]
        subgraph chimera21 ["chimera21 (GPU Node)"]
            DCGM["DCGM Exporter\n(:9401)"]
        end
    
        subgraph chimerahead ["chimerahead (CPU Node)"]
            NodeExp["Node Exporter\n(:9101)"]
            Gateway["SSH Forwarding Gateway\n(:9101, :9401)"]
        end
    end

    subgraph cs ["cs.umb.edu"]
      subgraph proxmox ["deploy@b6.cs.umb.edu (Proxmox VM)"]
          Prometheus["Prometheus Metrics Aggregation\n(:9090)"]
          Grafana["Grafana Dashboard\n(:3000)"]
      end
    end

    subgraph external ["Local Machine\nhost@<external ip>"]
        Browser["Web Browser\nhttp://localhost:3000/"]
    end

    %% Define Connections
    DCGM -- ":9401" --> Gateway
    NodeExp -- ":9101" --> Gateway
    
    Gateway -- "Forwarded\n(:9101, :9401)" --> Prometheus
    Prometheus --> Grafana
    
    Grafana -- "Forwarded\n(:3000)" --> Browser

    %% Styling (Optional, for better GitHub visibility)
    classDef nodeFill fill:#1f2328,stroke:#d0d7de,stroke-width:2px,color:#c9d1d9;
    classDef subFill fill:none,stroke:#8b949e,stroke-width:1px,stroke-dasharray: 5 5,color:#8b949e;
    
    class chimera21,chimerahead,proxmox,external subFill;
    class DCGM,NodeExp,Gateway,Prometheus,Grafana,Browser nodeFill;
```
