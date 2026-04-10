```mermaid
graph TD
    %% 定义样式
    classDef startEnd fill:#f9f,stroke:#333,stroke-width:2px;
    classDef process fill:#fff,stroke:#333,stroke-width:1px;
    classDef interface fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef decision fill:#fff9c4,stroke:#fbc02d,stroke-width:2px;
    classDef storyNode fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px;

    %% 流程节点
    Start((开始游戏)):::startEnd --> Route[选择路线]
    Route --> Tennis[分配 5 个网球归属]
    
    %% 新增：人物剧情生成阶段
    Tennis --> CharacterStories[<b>生成人物剧情</b><br/>每位角色不少于200字]
    CharacterStories --> Prologue[<b>进入序幕</b>]
    
    subgraph GameLoop [游戏核心循环]
        Prologue --> Panel[<b>显示游戏面板</b><br/>状态值更新 / 属性显示]
        Panel --> Action[选择下一天选项]
        Action --> TimeAdvance[时间线推进]
        TimeAdvance --> ContentGen[根据选择生成下一天内容]
        ContentGen --> Check{是否达到<br/>结局条件?}:::decision
    end

    %% 回路与结局
    Check -- 未达条件 --> Panel
    Check -- 满足条件 --> Ending[触发结局判定]
    
    Ending --> Final[生成结局并结束游戏]:::startEnd

    %% 备注
    style GameLoop fill:#f5f5f5,stroke:#999,stroke-dasharray: 5 5