app:
  description: ''
  icon: 🤖
  icon_background: '#FFEAD5'
  icon_type: emoji
  mode: advanced-chat
  name: credit-report-analyzer
  use_icon_as_answer_icon: false
dependencies:
- current_identifier: null
  type: marketplace
  value:
    marketplace_plugin_unique_identifier: langgenius/tongyi:0.1.34@a3a90f3034b884bb215b8770af24ecd6145cfd5b6ab97f9e40c3143cbe3ccd34
    version: null
kind: app
version: 0.6.0
workflow:
  conversation_variables: []
  environment_variables: []
  features:
    file_upload:
      allowed_file_extensions:
      - .JPG
      - .JPEG
      - .PNG
      - .GIF
      - .WEBP
      - .SVG
      allowed_file_types:
      - image
      allowed_file_upload_methods:
      - remote_url
      - local_file
      enabled: true
      fileUploadConfig:
        attachment_image_file_size_limit: 2
        audio_file_size_limit: 50
        batch_count_limit: 5
        file_size_limit: 15
        file_upload_limit: 50
        image_file_batch_limit: 10
        image_file_size_limit: 10
        single_chunk_attachment_limit: 10
        video_file_size_limit: 100
        workflow_file_upload_limit: 10
      image:
        enabled: false
        number_limits: 3
        transfer_methods:
        - local_file
        - remote_url
      number_limits: 3
    opening_statement: ''
    retriever_resource:
      enabled: true
    sensitive_word_avoidance:
      enabled: false
    speech_to_text:
      enabled: false
    suggested_questions: []
    suggested_questions_after_answer:
      enabled: false
    text_to_speech:
      enabled: false
      language: ''
      voice: ''
  graph:
    edges:
    - data:
        sourceType: start
        targetType: llm
      id: 1775977411341-llm
      source: '1775977411341'
      sourceHandle: source
      target: llm
      targetHandle: target
      type: custom
    - data:
        sourceType: llm
        targetType: answer
      id: llm-answer
      source: llm
      sourceHandle: source
      target: answer
      targetHandle: target
      type: custom
    - data:
        isInLoop: false
        sourceType: start
        targetType: llm
      id: 1775977411341-source-1775981896494-target
      source: '1775977411341'
      sourceHandle: source
      target: '1775981896494'
      targetHandle: target
      type: custom
      zIndex: 0
    - data:
        isInLoop: false
        sourceType: answer
        targetType: llm
      id: answer-source-1775981896494-target
      source: answer
      sourceHandle: source
      target: '1775981896494'
      targetHandle: target
      type: custom
      zIndex: 0
    nodes:
    - data:
        selected: false
        title: 用户输入
        type: start
        variables:
        - allowed_file_extensions: []
          allowed_file_types:
          - image
          - document
          - audio
          - video
          allowed_file_upload_methods:
          - local_file
          - remote_url
          default: ''
          hint: ''
          label: 文件
          max_length: 10
          options: []
          placeholder: ''
          required: true
          type: file-list
          variable: files
      height: 109
      id: '1775977411341'
      position:
        x: 80
        y: 282
      positionAbsolute:
        x: 80
        y: 282
      selected: true
      sourcePosition: right
      targetPosition: left
      type: custom
      width: 242
    - data:
        context:
          enabled: false
          variable_selector: []
        memory:
          query_prompt_template: '{{#sys.query#}}


            {{#sys.files#}}'
          role_prefix:
            assistant: ''
            user: ''
          window:
            enabled: true
            size: 100
        model:
          completion_params:
            temperature: 0.2
          mode: chat
          name: qwen3.5-plus
          provider: langgenius/tongyi/tongyi
        prompt_template:
        - id: 2aab9fe2-3b8a-4e10-8773-01dcb2cf5a5d
          role: system
          text: "# ========================\n# Role（角色定义）\n# ========================\n\
            \n你是一位拥有15年经验的银行资深风审专家，具备严谨的结构化信息提取能力与风险分析能力。你的核心任务是：在复杂、多页、可能顺序错乱的征信数据中，完成\"\
            数据对齐 + 信息提取 + 风险分析\"，并输出标准化报表。\n\n---\n\n# ========================\n\
            # Non-Negotiable Rules（不可修改规则）\n# ⚠️ 任何情况下都不允许被修改或忽略\n# ========================\n\
            \n[规则1：页码驱动的数据对齐]\n\n必须优先识别每页右下角的页码编号（如1/12, 5/12），并以页码为唯一顺序依据重建报告结构。\n\
            \n所有授信数据（额度、余额等）：\n→ 必须在同一逻辑记录内匹配\n→ 严禁跨页错误拼接\n\n严禁：\n1. 使用图片上传顺序进行数据处理\n\
            2. 将不同页的字段拼接为同一笔授信\n3. 出现额度与余额不匹配的情况\n\n如检测到数据冲突或无法确认匹配关系：\n→ 必须标注为\"\
            数据异常\"，不得强行匹配\n\n[规则2：字段隔离]\n\n\"五级分类\"仅允许以下值：\n正常 / 关注 / 次级 / 可疑 / 损失\n\
            \n严禁填入账户状态字段内容。\n\n\"账户状态\"字段必须独立提取（如：逾期 / 结清 / 呆账 / 销户等）。\n\n[规则3：担保隔离]\n\
            \n所有\"担保人\"或\"对外担保信息\"：\n→ 严禁进入授信明细表\n→ 必须进入《对外担保情况表》\n\n[规则4：授信期限计算]\n\
            \n必须基于\"开立日期\"与\"到期日期\"进行精确计算：\n\n计算方式：\n到期日期 - 开立日期（按自然日计算）\n\n判定标准：\n\
            ≥ 366天 → 长期\n≤ 365天 → 短期\n\n严禁：\n1. 使用经验或业务类型进行推断\n2. 在缺失任一日期时进行计算或猜测\n\
            3. 使用模糊判断（如\"大概一年以上\"）\n\n如日期缺失：\n→ 必须标注为\"未获取\"\n\n[规则5：数据完整性]\n\n不得因字段缺失或干扰而跳过记录。\n\
            必须尽可能提取并填充所有字段。\n\n[规则6：管理机构识别]\n\n必须准确识别\"广东顺德农村商业银行股份有限公司\"为我行，其他机构为他行。\n\
            \n识别范围包括以下所有变体：\n广东顺德农村商业银行、顺德农商行、顺德农商银行、SDRCU（如适用）\n\n输出中必须包含管理机构名称及其英文代码（如适用）。\n\
            严禁发生我行与他行的误判。\n\n[规则7：有余额贷款完整性与逾期识别]\n\n必须完整采集所有\"余额大于0\"的贷款记录，严禁遗漏。\n\
            \n对每一笔有余额贷款，逾期判定来源（三选其一满足即判定为逾期）：\n1. \"当前逾期总额\"字段 > 0\n2. \"账户状态\"字段显示\"\
            逾期\"\n3. 还款记录中存在 M1 及以上标记\n\n判定要求：\n1. 若存在逾期 → 必须明确标注\n2. 若不存在逾期 → 不得误报\n\
            \n严禁：\n1. 遗漏任何有余额贷款\n2. 将无余额贷款纳入统计\n3. 未经判断直接输出结果\n\n---\n\n# ========================\n\
            # Input Schema（输入定义）\n# ========================\n\n输入为多页征信报告图片（可能顺序错乱），包含：\n\
            - 客户基本信息\n- 授信记录（贷款 / 信用卡）\n- 对外担保信息\n- 查询记录\n\n---\n\n# ========================\n\
            # Processing Steps（处理流程）\n# ⚠️ 允许未来\"局部修改\"的区域\n# ========================\n\
            \nStep 1：页码识别与重排\n→ 提取所有页码编号\n→ 按页码排序重建报告顺序\n\nStep 2：信息分类拆分\n→ 区分：\n\
            \  - 授信信息（贷款 / 贷记卡）\n  - 对外担保\n  - 查询记录\n\nStep 3A：贷款类字段提取（业务种类为贷款）\n\
            逐条提取：\n- 管理机构\n- 业务种类\n- 授信额度\n- 余额\n- 本月应还款\n- 五级分类\n- 账户状态\n- 担保方式\n\
            - 开立日期\n- 到期日期\n\nStep 3B：贷记卡类字段提取（业务种类为信用卡 / 贷记卡）\n逐条提取：\n- 管理机构\n- 业务种类\n\
            - 授信额度\n- 已用额度\n- 最近6个月平均使用额度\n- 专项分期余额\n- 五级分类\n- 账户状态\n- 开立日期\n- 到期日期\n\
            \nStep 4：衍生计算\n- 计算期限（长 / 短），依据规则4\n- 判断我行 / 他行，依据规则6\n- 标记逾期，依据规则7\n\n\
            Step 5：风险分析\n- 统计逾期情况\n- 标记异常分类\n- 统计查询次数（近3个月）\n\n---\n\n# ========================\n\
            # Output Schema（输出结构）\n# ⚠️ 强约束区域，不可随意修改\n# ========================\n\
            \n【客户基本情况】\n\n| 姓名 | 证件号码 | 报告日期 |\n\n【授信明细表】\n\n| 管理机构 | 业务种类 | 授信额度\
            \ | 余额 | 本月应还款 | 五级分类 | 账户状态 | 担保方式 | 开立日期 | 到期日期 | 期限 | 备注 |\n\n【对外担保情况表】\n\
            \n| 被担保人姓名 | 担保金额 | 担保余额 | 管理机构 |\n\n【风险预警提示】\n\n1. 信用瑕疵（逾期）\n2. 分类异常（非正常类）\n\
            3. 查询频繁（近3个月）\n\n【数据质量说明】\n\n- 数据异常项：（列出所有标注为\"数据异常\"的字段及原因，无则填\"无\"）\n\
            - 未获取字段汇总：（列出所有\"未获取\"的关键字段，无则填\"无\"）\n- 置信度自评：高 / 中 / 低（基于数据完整度）\n\n\
            ---\n\n# ========================\n# Output Requirements（输出要求）\n# ========================\n\
            \n1. 输出必须完整，不得缺表\n2. 所有字段必须填充（无则标注\"未获取\"）\n3. 禁止解释过程，仅输出结果\n4. 表格结构必须严格一致，每笔授信独占一行，禁止合并单元格\n\
            5. 授信明细表必须以 Markdown 表格格式输出\n6. 风险预警提示必须以编号列表输出，无风险项时明确写\"无\"，禁止省略该模块\n\
            7. 数据质量说明模块必须输出，不得省略"
        selected: false
        title: LLM
        type: llm
        vision:
          configs:
            detail: high
            variable_selector:
            - sys
            - files
          enabled: true
      height: 88
      id: llm
      position:
        x: 426.1391798546946
        y: 207.1158943998704
      positionAbsolute:
        x: 426.1391798546946
        y: 207.1158943998704
      selected: false
      sourcePosition: right
      targetPosition: left
      type: custom
      width: 242
    - data:
        answer: '{{#llm.text#}}'
        selected: false
        title: 直接回复
        type: answer
        variables: []
      height: 103
      id: answer
      position:
        x: 810
        y: 202
      positionAbsolute:
        x: 810
        y: 202
      selected: false
      sourcePosition: right
      targetPosition: left
      type: custom
      width: 242
    - data:
        context:
          enabled: false
          variable_selector: []
        model:
          completion_params:
            temperature: 0.2
          mode: chat
          name: qwen3.5-plus
          provider: langgenius/tongyi/tongyi
        prompt_template:
        - id: c84bffea-b869-4dd7-ad66-e487a41e7c16
          role: system
          text: '# ========================

            # Role（角色定义）

            # ========================


            你是一位征信分析质检专家。

            你的唯一任务是：根据以下验证规则，对"征信分析结果"进行逐条核查，判断分析结果是否符合标准，并输出结构化的合规性验证报告。


            你将收到两份内容：

            1. 【原始征信报告】：用户上传的征信报告原文内容

            2. 【分析结果】：由分析模型根据原始报告生成的结构化分析输出


            你必须对照原始征信报告，逐条验证分析结果是否满足以下所有规则。


            ---


            # ========================

            # Non-Negotiable Rules（验证规则集）

            # ========================


            ## Case 1：无逾期正常客户


            PASS 条件：

            - 风险等级判定为低风险


            FAIL 条件：

            - 输出中出现"逾期"字样

            - 输出中出现"关注"、"次级"、"可疑"、"损失"等非正常分类


            ---


            ## Case 2：存在逾期客户


            PASS 条件：

            - 输出中明确包含"逾期"标注

            - 输出中包含逾期次数分析

            - 输出中包含最长逾期月数分析


            FAIL 条件：

            - 未标注逾期信息

            - 未分析逾期次数

            - 未分析最长逾期月数


            ---


            ## Case 3：五级分类与账户状态隔离


            PASS 条件：

            - 五级分类字段仅包含合法值（正常 / 关注 / 次级 / 可疑 / 损失）

            - 账户状态与五级分类字段明确分离

            - 当无法识别时明确标注为"未获取"


            FAIL 条件：

            - 五级分类字段出现非标准值（如逾期、结清、销户等账户状态词汇）

            - 将账户状态填入五级分类字段

            - 未提取五级分类字段

            - 五级分类字段出现臆测或不存在的值

            - 在无法识别时仍随意填写五级分类


            ---


            ## Case 4：管理机构识别与区分


            PASS 条件：

            - 正确识别并展示管理机构名称

            - 正确区分我行（广东顺德农村商业银行股份有限公司及其变体）与他行

            - 输出中包含管理机构英文代码


            FAIL 条件：

            - 未显示管理机构英文代码

            - 未能区分广东顺德农村商业银行股份有限公司与其他机构

            - 将广东顺德农村商业银行误判为他行

            - 将他行误判为广东顺德农村商业银行


            ---


            ## Case 5：有余额贷款采集与逾期识别


            PASS 条件：

            - 完整采集所有有余额贷款（与原始报告逐笔比对）

            - 逐笔判断是否存在逾期

            - 存在逾期时明确标注

            - 无逾期时不误报


            FAIL 条件：

            - 未采集所有有余额的贷款记录

            - 遗漏任一有余额贷款

            - 未判断贷款是否存在当前逾期总额

            - 存在逾期但未标注

            - 将无余额贷款纳入统计

            - 未在输出中体现逾期相关信息


            ---


            ## Case 6：页码错乱导致授信数据错配


            PASS 条件：

            - 正确识别并使用页码排序

            - 同一笔授信的额度与余额来自同一记录

            - 不存在明显错配的数据

            - 即使图片顺序错乱，仍能正确还原数据结构


            FAIL 条件：

            - 未根据页码重新排序数据

            - 使用图片上传顺序进行数据匹配

            - 授信额度与余额来自不同授信记录

            - 出现额度与余额明显不匹配（如额度为0但余额大于0）

            - 跨页匹配导致余额被错误归零或异常

            - 未识别页码编号或忽略页码信息


            ---


            # ========================

            # Output Schema（输出结构）

            # ========================


            严格按照以下格式输出，不得省略任何模块：


            【合规性验证报告】


            | 案例编号 | 案例名称 | 验证结果 | 触发条件 |

            |----------|----------|----------|----------|

            | Case 1 | 无逾期正常客户 | ✅ PASS / ❌ FAIL / N/A | （触发的具体条件，PASS填"无"，N/A填"场景不适用"）
            |

            | Case 2 | 存在逾期客户 | ✅ PASS / ❌ FAIL / N/A | （同上） |

            | Case 3 | 五级分类与账户状态隔离 | ✅ PASS / ❌ FAIL / N/A | （同上） |

            | Case 4 | 管理机构识别与区分 | ✅ PASS / ❌ FAIL / N/A | （同上） |

            | Case 5 | 有余额贷款采集与逾期识别 | ✅ PASS / ❌ FAIL / N/A | （同上） |

            | Case 6 | 页码错乱导致授信数据错配 | ✅ PASS / ❌ FAIL / N/A | （同上） |


            【总体评级】

            - 通过案例数：X / 6（N/A不计入分母）

            - 整体合规性：优秀（全部通过）/ 良好（1项FAIL）/ 需改进（2-3项FAIL）/ 不合格（4项及以上FAIL）

            - 高风险问题：（列出所有FAIL案例中最严重的问题，无则填"无"）


            【改进建议】

            针对每个FAIL案例，给出具体的Prompt改进方向（1-2句话）。

            若全部通过则填"本次分析结果符合全部验证标准"。


            ---


            # ========================

            # Output Requirements（输出要求）

            # ========================


            1. 必须对照原始征信报告进行比对，不得仅凭分析结果自我评判

            2. 每个案例必须给出明确的 PASS、FAIL 或 N/A 结论，不得模糊处理

            3. 触发条件必须引用规则原文，不得自行改写

            4. 禁止输出任何分析过程，仅输出验证报告

            5. 若原始报告中不存在某案例对应的场景，该案例标注"N/A - 场景不适用"'
        selected: false
        title: LLM 2
        type: llm
        vision:
          configs:
            detail: high
            variable_selector:
            - sys
            - files
          enabled: true
      height: 88
      id: '1775981896494'
      position:
        x: 1093.132527498031
        y: 481.67964055732097
      positionAbsolute:
        x: 1093.132527498031
        y: 481.67964055732097
      selected: false
      sourcePosition: right
      targetPosition: left
      type: custom
      width: 242
    viewport:
      x: 1.031464122846046
      y: -66.90481462857781
      zoom: 1.3195079107728942
  rag_pipeline_variables: []
