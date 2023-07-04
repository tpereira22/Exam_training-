#include <unistd.h>
#include <stdarg.h>

void	printnum(long long int num, int base, int *len)
{
	char	hex[] = "0123456789abcdef";

	if (num < 0)
	{
		*len += write(1, "-", 1);
		num *= -1;
	}
	if (num >= base)
		printnum(num / base, base, len);
	*len += write(1, &hex[num % base], 1);
}

int	printstr(char *str)
{
	int	i;

	if (!str)
	{
		write(1, "(null)", 6);
		return (6);
	}
	i = -1;
	while (str[++i])
		write(1, &str[i], 1);
	return (i);
}

int	ft_printf(const char *str, ...)
{
	va_list	args;
	int	i;
	int	len;

	va_start(args, str);
	i = 0;
	len = 0;
	while (str[i])
	{
		if (str[i] == '%' && (str[i + 1] == 's' || str[i + 1] == 'd' || str[i + 1] == 'x'))
		{
			i++;
			if (str[i] == 's')
				len += printstr(va_arg(args, char *));
			else if (str[i] == 'd')
				printnum(va_arg(args, long long int), 10, &len);
			else if (str[i] == 'x')
				printnum(va_arg(args, unsigned int), 16, &len);
		}
		else
			len += write(1, &str[i], 1);
		i++;
	}
	va_end(args);
	return (len);
}
