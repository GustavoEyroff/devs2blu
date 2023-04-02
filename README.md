static string SearchingChallenge(string str)
{
    var words = str.Split(' ');
    
    var maxRepeatedLetters = -1;
    var wordWithMaxRepeatedLetters = "";

    foreach (var word in words)
    {
        var repeatedLetters = word
            .GroupBy(c => c)
            .Select(g => g.Count())
            .Max();
            
        if (repeatedLetters > maxRepeatedLetters)
        {
            maxRepeatedLetters = repeatedLetters;
            wordWithMaxRepeatedLetters = word;
        }
    }

    if (maxRepeatedLetters == 1)
    {
        return "-1";
    }
    else
    {

        var finalString = new string(wordWithMaxRepeatedLetters
            .Where(c => !char.IsWhiteSpace(c) && !char.IsPunctuation(c) && !char.IsSymbol(c))
            .Select(c => char.ToLower(c))
            .Distinct()
            .Where(c => !ChallengeToken.Contains(char.ToLower(c)))
            .ToArray());

        if (finalString == "")
        {
            return "VAZIA";
        }
        else
        {
            // Retorna a nova string final
            return finalString;
        }
    }
}
