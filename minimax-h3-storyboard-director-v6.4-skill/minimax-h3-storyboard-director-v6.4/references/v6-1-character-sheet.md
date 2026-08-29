# V6.1 Face-Master Character Reference｜V6.4 User-Facing Output Rules

## 1. Goal

Each important character ultimately occupies **one reference image** for MiniMax H3 character identity generation. The visual structure remains V6.1:

- large authoritative frontal **Master Face** on the left;
- left 45° Rotation Anchor on the upper-right-left;
- right 45° Rotation Anchor on the upper-right-right;
- front Body Appearance on the lower-right-left, with no identifiable face;
- back Body Appearance on the lower-right-right, preserving the rear hairstyle but never revealing the face.

Recommended canvas: **2304×1296, 16:9 horizontal, seamless pure white background, no visible dividers, labels, text, watermark, or logo**.

Identity hierarchy is fixed:

`Master Face >>> Rotation Anchors >>> Body Appearance`

Makeup, hairstyle, hair color, age impression, skin tone, and stable styling must remain unchanged across all zones.

---

## 2. Two Output Modes

### Mode A — 完整单 Prompt（默认）

This is the normal user-facing behavior.

When the user uploads a raw character reference and asks for a character Sheet, **output exactly one complete prompt** that describes the whole Sheet. The user should be able to copy it once and generate the full reference image.

Do **not** output the internal sub-prompts as separate visible sections. In particular, do not default to:

- `左45° Rotation Anchor Prompt`
- `右45° Rotation Anchor Prompt`
- `正面 Body Appearance Prompt`
- `背面 Body Appearance Prompt`

Those remain internal rules used to compose the single final prompt.

### Mode B — 严格 Face-Master 分区拼版（仅用户明确要求时）

Only expose separate auxiliary prompts when the user explicitly asks for strict pixel-preserved Master Face production, separate region generation, or final compositing.

In strict Mode B:

1. preserve the original Master Face pixels without generative modification;
2. generate left 45° separately;
3. generate right 45° separately;
4. generate front Body Appearance separately;
5. generate back Body Appearance separately;
6. composite all five areas into one 2304×1296 image.

---

## 3. 默认完整 V6.1 Character Sheet Prompt 模板

When needed, fill the bracketed character details and return the following as **one continuous prompt block**:

```text
使用用户提供的原始正面人物参考图作为该角色唯一、最高优先级的人物身份来源，生成一张完整的 V6.1 Face-Master Character Reference Sheet。最终只输出一张完整角色参考图，不拆分为多个独立图片或多个提示词。

画布固定为 2304×1296，16:9 横向，纯白无缝背景。整张图中只有同一个角色，不出现第二个人物，不显示任何格线、边框、标题、角色名、角度标签、文字、水印、Logo、箭头或说明标记。

整体版式：左侧约占总宽度 44%–48%，放置最大、最清晰的正面 Master Face；右侧剩余区域分为四个自然排布的辅助视图，右上左为左45° Rotation Anchor，右上右为右45° Rotation Anchor，右下左为正面 Body Appearance，右下右为背面 Body Appearance。五个视图自然分布于同一连续白色背景上，不出现可见分隔线。

【Master Face｜唯一身份真值】
左侧最大正面人物必须严格继承用户原始参考图中的人物身份、年龄状态、脸型、头骨比例、额头、眉形、眼型、眼距、眼睛真实大小、鼻梁、鼻尖、鼻翼、嘴唇、人中、下巴、下颌、颧骨、肤色、发际线、发型、发色、妆容强度以及自然面部不对称特征。不要重新美化，不改变人物妆造，不改变年龄感，不改变五官比例，不把人物生成成“相似但不同的人”。Master Face 是整张图唯一且最高优先级的人物身份定义。

【左45° Rotation Anchor】
右上左显示同一人物头部向她/他自己的左侧自然旋转约45°后的头肩肖像，鼻尖明确朝画布左侧。它不是新的身份样本，只是 Master Face 同一个真实头部的旋转状态。只允许旋转产生的真实透视、遮挡、脸颊可见面积、眼睛透视宽度、鼻梁侧向投影、耳朵可见程度和下颌投影发生变化。禁止眼睛变大、鼻子变挺、鼻尖变小、脸变窄、下巴变尖、嘴唇变厚、颧骨重新塑形、年龄漂移、肤色变化、妆容变化或发型变化。Projection changes only. Identity geometry must remain unchanged.

【右45° Rotation Anchor】
右上右显示同一人物头部向她/他自己的右侧自然旋转约45°后的头肩肖像，鼻尖明确朝画布右侧，并与左45°形成相反方向。它同样只负责转头几何，不得重新解释人物身份。保持与 Master Face 完全一致的脸型、头骨比例、眉眼、眼距、鼻梁、鼻尖、鼻翼、嘴唇、人中、下巴、下颌、颧骨、肤色、年龄感、发际线、发型、发色和妆容。只允许真实旋转产生的透视和遮挡变化。Projection changes only. Identity geometry must remain unchanged.

【正面 Body Appearance｜无脸】
右下左显示同一角色的正面身体造型，只负责身体比例和服装造型，不负责人物面部身份。构图从颈根或锁骨附近开始，完整头部与所有可识别面部结构位于画框之外；不得出现眼睛、眉毛、鼻子、嘴、下巴或任何清晰小脸。人物自然正面站立，双臂自然放松。锁定角色设定中的[体型]、[肩宽]、[胸腰臀比例]、[手臂和腿部比例]、[服装正面]、[材质]、[腰线]、[裤型/裙型]、[配饰]。只要不压缩脸部区域，可展示完整全身；若空间不足，优先裁掉小腿和鞋，而不是缩小 Master Face 或两个45°脸。

【背面 Body Appearance｜不露脸】
右下右显示同一角色严格背对相机的身体造型，保留完整后脑和发型背面，但绝不出现脸、脸颊、眼睛、鼻子、嘴唇或侧脸；禁止回头和半回头。背面发型必须是 Master Face 当前发型的真实物理背面，保持相同的头顶分线、扎发位置、马尾高度、头发长度、发量、卷直程度、发尾位置和发色；禁止重新设计更长、更厚、更卷或更蓬松的头发。锁定[服装背面]、[肩背比例]、[腰臀比例]、[背面裤型/裙型]、[背部配饰]。

【全局身份与妆造锁】
五个区域必须明确属于同一个角色。人物妆容、发型、发色、年龄感、肤色和稳定服装设定不得在不同视图中变化。身份优先级始终为：Master Face >>> Rotation Anchors >>> Body Appearance。若任何辅助视图与 Master Face 出现冲突，一律以 Master Face 为准。

【摄影与画面】
真人写实摄影，清晰自然皮肤纹理，柔和均匀摄影棚光线，中性白平衡，所有区域保持一致的摄影观感和基础曝光。人物姿态自然，不进行夸张表演。

【禁止】
禁止第二人物，禁止重复人物，禁止身份漂移，禁止左右45°重新美容，禁止年龄漂移，禁止妆容变化，禁止发型变化，禁止肤色变化，禁止正面身体出现小脸，禁止背面人物回头露脸，禁止背面发型重新设计，禁止动漫风，禁止塑料皮肤，禁止明显解剖错误，禁止可见格线、边框、卡片、标题、标签、文字、水印、Logo。
```

### Mandatory UX rule

After producing the unified prompt, stop and ask the user to confirm/generate the Sheet. Do not append the four internal sub-prompts unless the user has explicitly selected Mode B.

---

## 4. Internal Rules for Rotation / Body Zones

The following rules are **internal guidance** for the agent. They may be used to build the Mode A unified prompt, but should not normally be displayed as separate deliverables.

### Left 45° internal rule
- same physical identity as Master Face;
- nose points to canvas-left;
- projection/occlusion changes only;
- no beautification or makeup/hair drift.

### Right 45° internal rule
- same physical identity as Master Face;
- nose points to canvas-right;
- opposite direction from left 45°;
- projection/occlusion changes only.

### Front Body internal rule
- face is absent, not merely blurred;
- start around neck root/clavicle;
- body/costume reference only.

### Back Body internal rule
- strict back view;
- keep complete rear hairstyle structure;
- no cheek, profile, eye, nose, mouth, or head turn.

---

## 5. Reference Interpretation for Later H3 Character Generation

```text
@图片X：角色[角色名]的 V6.1 Face-Master Character Reference Sheet。

左侧最大正面人物照片是唯一且最高优先级的 Master Face，用于定义人物真实身份。右上两张45°脸仅作为 Rotation Anchors，补充人物向左/向右转头时的面部透视结构，不得覆盖、重新解释或重新设计 Master Face。右下正面/背面身体仅用于锁定体型、身体比例、服装、材质、配饰以及背面发型结构；身体区域不得参与人物面部身份定义。

任何区域存在差异时，始终以左侧 Master Face 为最高优先级。
```

## 6. Acceptance Checklist

- [ ] Default output was one unified Sheet prompt, not four visible sub-prompts
- [ ] Only if user explicitly requested strict composite mode were the sub-prompts exposed
- [ ] Master Face is the clear identity authority
- [ ] Left 45° points canvas-left; right 45° points canvas-right
- [ ] Rotation views preserve makeup, hairstyle, age impression, skin tone, and identity geometry
- [ ] Front body has no identifiable face
- [ ] Back body never reveals face/profile
- [ ] Rear hairstyle matches the Master Face hairstyle physically
- [ ] Final image remains one 16:9 character reference image
- [ ] No visible divider, text, labels, watermark, or logo
