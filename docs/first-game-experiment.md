# 首个游戏站实验清单

> 目标：选定一个游戏后，用最小范围验证“选题 → 内容 → SEO → 部署”的完整闭环。首轮不做用户系统、数据库或 CMS。

## 开始前准备

先确认以下信息，缺失项可以标记为“暂不启用”，不要使用模板里的演示值：

| 项目 | 需要准备的内容 |
| --- | --- |
| 游戏 | 正式名称、平台、开发商、类型、发布日期 |
| 官方来源 | 官网或商店页、官方 Wiki、Discord、更新日志 |
| 目标市场 | 首发语言、主要国家、目标玩家类型 |
| 站点 | 暂定站名、候选域名、品牌主色 |
| 内容 | 4–6 个分类、首批 5–10 篇文章题目 |
| 素材 | 1200×630 Hero/分享图、Logo、favicon、文章封面 |

游戏截图、Logo 和角色素材需要符合该游戏的粉丝内容或品牌使用政策。模板的 MIT 许可证只覆盖模板代码，不覆盖第三方游戏素材。

## 建议的首轮范围

- 英文作为默认语言；首轮先移除未实际维护的其他语言。
- 保留 4 个以内的核心分类，例如 Guides、Codes、Items、Bosses。
- 首批发布 5–10 篇有真实来源、能持续更新的内容。
- 开启站内搜索；评论、广告和统计先保持关闭。
- 使用 Cloudflare Pages 免费域名完成验证，再决定是否购买自定义域名。

## 套用顺序

1. 在 `dev` 分支运行 `pnpm apply-template`，填写游戏和站点基础信息。
2. 检查 `src/config/site.ts`，删除不存在的社交链接。
3. 确认 `src/config/navigation.ts` 的分类与内容目录完全一致。
4. 替换 `src/locales/en.json` 中所有首页、FAQ、页脚和 SEO 文案。
5. 删除 `src/content/wiki/` 下的 Anvil Quest 演示文章，写入真实文章。
6. 替换 `public/` 中的 Hero、favicon、PWA 图标和 `manifest.json`。
7. 替换首页视频 ID；没有合适视频时移除视频模块数据。
8. 搜索演示残留：`Anvil Quest`、`Forge Studios`、`example.com`、占位视频 ID。
9. 运行完整验证，通过后再合并到 `main`。

## 本地验收

```bash
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

还要在浏览器中实际检查：首页、每个分类、至少一篇文章、搜索、404、亮暗主题，以及桌面端和移动端是否存在横向溢出或无效链接。

## 部署准备

Cloudflare Pages 使用以下设置：

| 设置 | 值 |
| --- | --- |
| Production branch | `main` |
| Preview branch | `dev` |
| Build command | `pnpm build` |
| Output directory | `dist` |
| Node | `22` |
| `SITE_URL` | 当前部署的完整 HTTPS 地址 |

本 Fork 不提交 `wrangler.toml`，环境变量统一在 Cloudflare dashboard 管理。评论、广告、Analytics 和 Search Console 均为可选项，首轮留空不会影响站点运行。

## 合并到 main 前

- 页面里不存在虚构游戏和占位链接。
- sitemap、robots、canonical 和分享图全部指向自己的站点。
- 所有文章事实都有来源，兑换码和版本信息标明更新时间。
- 法律声明明确这是非官方粉丝站。
- 构建与测试通过，Cloudflare Preview 已完成浏览器验收。
- 确认没有把 `.env`、广告密钥或其他凭据提交到仓库。
