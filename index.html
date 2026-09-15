export default async function handler(req, res) {
    if (req.method !== 'POST') {
        return res.status(405).json({ error: 'الطريقة غير مسموحة' });
    }

    const { message, lang } = req.body || {};

    if (!message || typeof message !== 'string' || !message.trim()) {
        return res.status(400).json({ error: 'الرجاء كتابة سؤال.' });
    }

    let languageInstruction = 'Arabic';
    if (lang === 'fr') languageInstruction = 'French';
    if (lang === 'en') languageInstruction = 'English';

    const fullPrompt = `أنت مساعد ذكي ونظام خبير في دليل الاستعمال. أجب باحترافية، باختصار، وبشكل مباشر باللغة: ${languageInstruction}.\n\nسؤال المستخدم: ${message}`;

    const apiKey = process.env.GEMINI_API_KEY;

    if (!apiKey) {
        console.error('GEMINI_API_KEY is missing');
        return res.status(200).json({
            reply: 'عذراً، الخدمة غير متاحة حالياً. يرجى المحاولة لاحقاً.'
        });
    }

    const callGemini = async () => {
        const response = await fetch(
            `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`,
            {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    contents: [{ parts: [{ text: fullPrompt }] }],
                    generationConfig: { temperature: 0.7, maxOutputTokens: 800 }
                })
            }
        );
        if (!response.ok) {
            const errBody = await response.text();
            throw new Error(`Gemini API ${response.status}: ${errBody}`);
        }
        return response.json();
    };

    try {
        let data;
        try {
            data = await callGemini();
        } catch (firstError) {
            console.warn('First attempt failed, retrying...', firstError.message);
            await new Promise(r => setTimeout(r, 800));
            data = await callGemini();
        }

        const botReply = data?.candidates?.[0]?.content?.parts?.[0]?.text;
        if (!botReply) throw new Error('Empty response from Gemini');

        return res.status(200).json({ reply: botReply.trim() });

    } catch (error) {
        console.error('Gemini API failed after retry:', error.message);
        return res.status(200).json({
            reply: 'عذراً، لم أتمكن من معالجة طلبك حالياً. حاول مرة أخرى.'
        });
    }
}
