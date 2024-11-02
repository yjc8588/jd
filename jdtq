// Loon 脚本入口
(async () => {
    const url = 'https://sub.lingche.icu/api/v1/client/subscribe?token=48e95450735e7d06d61b56f9bdb349fc';
    const $ = $loon; // Loon 提供的工具对象

    // 获取远程订阅内容
    const response = await $.http.get({
        url: url,
        headers: {
            'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36'
        }
    });

    if (response.status !== 200) {
        console.error('无法获取订阅链接内容，请检查链接是否有效');
        return;
    }

    // 解码订阅内容
    const decodedContent = atob(response.body);

    // 解析节点信息
    const nodes = decodedContent.split('\n').filter(link => {
        return link.startsWith('vmess://') || link.startsWith('vless://') || link.startsWith('ss://') || link.startsWith('trojan://');
    });

    if (nodes.length === 0) {
        console.error('订阅内容中没有有效节点');
        return;
    }

    // 输出提取的节点到 Loon 的日志
    console.log('提取的节点信息:');
    nodes.forEach(node => console.log(node));

    // 将解析出的节点信息返回给 Loon
    const nodeResult = nodes.join('\n');
    $done({
        nodes: nodeResult
    });
})();
